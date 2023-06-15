
#### VIETNAM'S PHONE_REGEX
```bash
'^(0[3|5|7|8|9])+([0-9]{8})$'
```

#### VN BANKS
```python
from django.utils.translation import gettext as _

list_bank_trans_vi = (
	(("ABB"), ("An Binh Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần An Bình")),
	(("ACB"), ("Asia Commercial Joint-stock Bank - Ngân hàng thương mại cổ phần Á châu")),
	(("AGRIBANK"), (
		"Vietnam Bank for Agriculture and Rural Development - Agribank - Ngân hàng nông nghiệp và phát triển nông thông Việt Nam")),
	(("BACABANK"), ("Bac A Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Bắc Á")),
	(("BID"), (
		"Joint Stock Commercial Bank for Investment and Development of Vietnam - Ngân hàng thương mại cổ phần đầu tư và phát triển Việt Nam")),
	(("CTG"), (
		"Vietnam Joint-Stock Commercial Bank for Industry and Trade - Ngân hàng thương mại cổ phần công thương Việt Nam")),
	(("EIB"),
	 ("Vietnam Export Import Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần xuất nhập khẩu Việt Nam")),
	(("HDBANK"),
	 ("Ho Chi Minh City Development Joint Stock Commercial Bank - Ngân hàng thương mại cổ phần phát triển TP.HCM")),
	(("KLB"), ("Kien Long Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Kiên Long")),
	(("LIENVIET"), ("Lien Viet Post Joint Stock Commercial Bank - Ngân hàng thương mại cổ phần bưu điện Liên Việt")),
	(("MBB"), ("Military Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần quân đội")),
	(("MSB"), ("Vietnam Maritime Commercial Stock Bank - Ngân hàng thương mại cổ phần hàng hải Việt Nam")),
	(("NAMA"), ("Nam A Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Nam Á")),
	(("NCB"), ("National Citizen Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần quốc dân")),
	(("OCB"), (
		"Orient Commercial Joint Stock Bank-Ngan Hang Thuong Mai Co Phan Phuong Dong - Ngân hàng thương mại cổ phần Phương Đông")),
	(("PGBANK"),
	 ("Petrolimex Group Commercial Joint Stock Bank (The) - Ngân hàng thương mại cổ phần xăng dầu PETROLIMEX")),
	(("PVCOMBANK"), ("Vietnam Public Joint Stock Commercial Bank - Ngân hàng thương mại cổ phần đại chúng Việt Nam")),
	(("SCB"), ("Sai Gon Joint Stock Commercial Bank - Ngân hàng thương mại cổ phần Sài Gòn")),
	(("SEABANK"), ("Southeast Asia Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Đông Nam Á")),
	(("SGB"), ("Saigon Bank for Industry and Trade - Ngân hàng thương mại cổ phần Sài Gòn công thương")),
	(("SHB"), ("Saigon - Hanoi Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Sài Gòn - Hà Nội")),
	(("STB"),
	 ("Saigon Thuong Tin Commercial Joint-Stock Bank- SACOMBANK - Ngân hàng thương mại cổ phần Sài Gòn thương tín")),
	(("TCB"),
	 ("Vietnam Technological and Commercial Joint-Stock Bank - Ngân hàng thương mại cổ phần kỹ thương Việt Nam")),
	(("TPB"), ("Tien Phong Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Tiên Phong")),
	(("VCB"), (
		"Joint Stock Commercial Bank for Foreign Trade of Vietnam- VIETCOMBANK - Ngân hàng thương mại cổ phần ngoại thương Việt Nam")),
	(("VIB"), ("VietNam International Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần quốc tế Việt Nam")),
	(("VIETABANK"), ("Vietnam Asia Commercial Joint - Ngân hàng thương mại cổ phần Việt Á")),
	(("VIETCAPITALBANK"), ("Viet Capital Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Bản Việt")),
	(("VPB"), ("Vietnam Prosperity Joint Stock Commercial Bank - Ngân hàng thương mại cổ phần Việt Nam thịnh vượng")),
	(("VIETBANK"),
	 ("Vietnam Thuong Tin Commercial Joint Stock Bank - Ngân hàng thương mại cổ phần Việt Nam Thương Tín")),
)

vn_banks = (
	(("ABB"), _("An Binh Commercial Joint Stock Bank")),
	(("ACB"), _("Asia Commercial Joint-stock Bank")),
	(("AGRIBANK"), _("Vietnam Bank for Agriculture and Rural Development - Agribank")),
	(("BACABANK"), _("Bac A Commercial Joint Stock Bank")),
	(("BID"), _("Joint Stock Commercial Bank for Investment and Development of Vietnam")),
	(("CTG"), _("Vietnam Joint-Stock Commercial Bank for Industry and Trade")),
	(("EIB"), _("Vietnam Export Import Commercial Joint Stock Bank")),
	(("HDBANK"), _("Ho Chi Minh City Development Joint Stock Commercial Bank")),
	(("KLB"), _("Kien Long Commercial Joint Stock Bank")),
	(("LIENVIET"), _("Lien Viet Post Joint Stock Commercial Bank")),
	(("MBB"), _("Military Commercial Joint Stock Bank")),
	(("MSB"), _("Vietnam Maritime Commercial Stock Bank")),
	(("NAMA"), _("Nam A Commercial Joint Stock Bank")),
	(("NCB"), _("National Citizen Commercial Joint Stock Bank")),
	(("OCB"), _("Orient Commercial Joint Stock Bank-Ngan Hang Thuong Mai Co Phan Phuong Dong")),
	(("PGBANK"), _("Petrolimex Group Commercial Joint Stock Bank (The)")),
	(("PVCOMBANK"), _("Vietnam Public Joint Stock Commercial Bank")),
	(("SCB"), _("Sai Gon Joint Stock Commercial Bank")),
	(("SEABANK"), _("Southeast Asia Commercial Joint Stock Bank")),
	(("SGB"), _("Saigon Bank for Industry and Trade")),
	(("SHB"), _("Saigon - Hanoi Commercial Joint Stock Bank")),
	(("STB"), _("Saigon Thuong Tin Commercial Joint-Stock Bank- SACOMBANK")),
	(("TCB"), _("Vietnam Technological and Commercial Joint-Stock Bank")),
	(("TPB"), _("Tien Phong Commercial Joint Stock Bank")),
	(("VCB"), _("Joint Stock Commercial Bank for Foreign Trade of Vietnam- VIETCOMBANK")),
	(("VIB"), _("VietNam International Commercial Joint Stock Bank")),
	(("VIETABANK"), _("Vietnam Asia Commercial Joint")),
	(("VIETCAPITALBANK"), _("Viet Capital Commercial Joint Stock Bank")),
	(("VPB"), _("Vietnam Prosperity Joint Stock Commercial Bank")),
	(("VIETBANK"), _("Vietnam Thuong Tin Commercial Joint Stock Bank")),
)

```

#### VIETNAM E-WALLETS

```python
wallet_vn = [
    "MoMo",
    "ViettelPay",
    "ZaloPay",
    "VTC Pay ",
    "Payoo ",
    "ShopeePay",
    "VNPay",
    "Moca",
    "Vimo",
    "VinID",
]
```