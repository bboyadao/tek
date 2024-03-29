## 1. SAME KIND.
Base models
```python
# /product/models.py
from django.db import models


class Product(models.Model):
	name = models.CharField(max_length=255)


class Variant(models.Model):
	name = models.CharField(max_length=255)
	product = models.ForeignKey(Product, on_delete=models.CASCADE)
	price = models.PositiveIntegerField()

```
i got my app name is `product` and register in `INSTALLED_APPS` settings

`price = models.PositiveIntegerField()` need to be decimal\
there are db schema having some primitive type: char, int, varchar... another.\
But for all it's just number and text.\
Just simply to change the type to `DecimalField`
```python
class Variant(models.Model):
	name = models.CharField(max_length=255)
	product = models.ForeignKey(Product, on_delete=models.CASCADE)
	price = models.DecimalField(decimal_places=3, max_digits=999)
```
and then run make migration
```shell
python manage.py makemigrations product
```

```python
# /product/migrations/0002_alter_variant_price.py
# Generated by Django 4.1.7 on 2023-02-23 22:35

from django.db import migrations, models


class Migration(migrations.Migration):

    dependencies = [
        ("product", "0001_initial"),
    ]

    operations = [
        migrations.AlterField(
            model_name="variant",
            name="price",
            field=models.DecimalField(decimal_places=3, max_digits=999),
        ),
    ]
```
Django will automate generate a new migration file base on our behavior as you can see above.\
And then migrate it's 
```shell
python manage.py migrate product
```
Now just find where we implemented this field and do more change logic, syntax, etc...\
Everything will work.
##### Well it's just a simple case, because it is the same type in general: `NUMBER`

## 2. NEW FIELD BASED ON EXISTED FIELD.
Now we do harder from `int` to `datetime`\
I have a subscribes app like product above too.
```python
# subscribe/models.py
class Subscriber(models.Model):
	email = models.EmailField()
	age = models.SmallIntegerField()
```
This model run so long ago and have a thousand records in it\
For more logical and painful of code it's should be date of birth(DOB)\
I have to migrate existed data to new type right?

```python
class Subscriber(models.Model):
	email = models.EmailField()
	age = models.SmallIntegerField()
	dob = models.DateField()
```
Well just add a dob field and run make & migrate.

```shell
python manage.py makemigrations
It is impossible to add a non-nullable field 'dob' to subscriber without specifying a default. This is because the database needs something to populate existing rows.
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit and manually define a default value in models.py.
Select an option: 
```
Ahhhh that it.\
If i place `null=True` to attribute in the model's field that's will work perfectly within null value. But for what?

So now we have to do more calculate for it.\
Make a fresh migrate app from django template.
```shell
python manage.py makemigrations subscribe --name convert_age_dob --empty
```
and the output
```shell
Migrations for 'subscribe':
  subscribe/migrations/0002_convert_age_dob.py
```
```python
# subscribe/migrations/0002_convert_age_dob.py
# Generated by Django 4.1.7 on 2023-02-23 23:09

from django.db import migrations


class Migration(migrations.Migration):

    dependencies = [
        ("subscribe", "0001_initial"),
    ]

    operations = []
```
Here the battlefield\
Need a function convert from age to DOB right ?

```python
from django.utils import timezone

def age_to_dob(apps, schema_editor):
    Subscriber = apps.get_model('subscribe', 'Subscriber')
    today = timezone.now()
    for sub in Subscriber.objects.all():
        sub.dob = today.replace(year=today.year-sub.age)  # that too dirty but i'll fix it later
        sub.save()
```
and let operation run it

```python
operations = [
        migrations.RunPython(age_to_dob, migrations.RunPython.noop),
]
```
`migrations.RunPython.noop` is the step backward if we revert the migration. so for do nothing i added `noop`
###### Now my completed migration file is:
```python
# Generated by Django 4.1.7 on 2023-02-23 23:09

from django.db import migrations, models
from django.utils import timezone


def age_to_dob(apps, schema_editor):
    Subscriber = apps.get_model('subscribe', 'Subscriber')
    today = timezone.now()
    for sub in Subscriber.objects.all():
        sub.dob = today.replace(year=today.year-sub.age)  # that too dirty but i'll fix it later
        sub.save()


class Migration(migrations.Migration):

    dependencies = [
        ("subscribe", "0001_initial"),
    ]

    operations = [
        migrations.AddField(
            model_name='Subscriber',
            name='dob',
            field=models.DateField(null=True, default=None),
            preserve_default=False,
        ),
        
        migrations.RunPython(age_to_dob, migrations.RunPython.noop),

        migrations.AlterField(
            model_name='Subscriber',
            name='dob',
            field=models.DateField(),
            preserve_default=True,
        ),
    ]

```
well a little big rigt ?\
we have `migrations.AddField` anf `migrations.AlterField` it's just the trick to bypass not-null value from django migrate schema. cuz we need this always having data\
Otherwise, you will get the error `django.db.utils.IntegrityError: NOT NULL constraint failed:...`

and run migrate this file.

## 3. SAME FIELD AND DIFFERENT TYPE.
>This is the hard part on refactor operation a projects.\
>Added new field and then copy data in to it will make many critical error on release and if we run in `container` we have to create lots of releases that's increment time and effort!

As all we know. django model have `pk` default for your record, it is a `biginterger` and have `auto increment` on the back.\
Now if we expose this to the public like id of post or user id. This way is the door to invites crawler get my own data. Cuz it's predictable.\
So it must be unpredictable, by using uuid or other algorythm to create identify instead.\
I got my user model here

```python
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):
	alias = models.CharField(max_length=255)
    ...	
```
That run quite long ago and got a lot of users\ 
At this if we call `.id` or `.pk` will return int for each record.\
And tons of code implemented before take time to refactor. Would you add more field like `uuid` and then go to fix, add, delete old logic ???\
NOOOOOOOOOOOOOOO! imma lazy guy. And i impl like this.
```python
import uuid
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    alias = models.CharField(max_length=255)
    ...
```
Then make a function generate new id inside of migration stage.
make it.
```python
user/migrations/0002_alter_user_id.py
# Generated by Django 4.1.7 on 2023-02-24 01:14

from django.db import migrations, models
import uuid


class Migration(migrations.Migration):

    dependencies = [
        ("user", "0001_initial"),
    ]

    operations = [
        migrations.AlterField(
            model_name="user",
            name="id",
            field=models.UUIDField(
                default=uuid.uuid4, editable=False, primary_key=True, serialize=False
            ),
        ),
    ]
```
Django generated it for me. but it just applies to new record which insert in the future. what should I do for existed id.\

So i apply my flow here and run it without any error.
```python
from django.db import migrations, models
import uuid


def create_uuid(apps, schema_editor):
    User = apps.get_model('user', 'User')
    for user in list(User.objects.all()):
        user.id = uuid.UUID(int=user.id)
        user.save()


class Migration(migrations.Migration):

    dependencies = [
        ("user", "0001_initial"),
    ]

    operations = [
        # add new one
        migrations.AddField(
            model_name='user',
            name='uuid',
            field=models.UUIDField(null=True),
        ),
        # seed new one
        migrations.RunPython(create_uuid, migrations.RunPython.noop),

        # change attributes
        migrations.AlterField(
            model_name='user',
            name='uuid',
            field=models.UUIDField(
                default=uuid.uuid4, editable=False, primary_key=True, serialize=False
            ),
        ),

        # remove old one
        migrations.RemoveField('User', 'id'),

        # rename to new
        migrations.RenameField(
            model_name='User',
            old_name='uuid',
            new_name='id'
        ),

        # Update attributes
        migrations.AlterField(
            model_name='user',
            name='id',
            field=models.UUIDField(
                primary_key=True, default=uuid.uuid4, serialize=False, editable=False
            ),
        ),
    ]
```