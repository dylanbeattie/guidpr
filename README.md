# GuiDPR : GUID + GDPR
GUID + GDPR = GuiDPR. Stable, plausible fake data based on GUID database IDs.

**Deterministic:** The same GUIDs always produce the same results.

**Plausible:** Names, email addresses, streets and phone numbers look convincing.

**Secure:** Data is generated from GUIDs. No way to get back to the original names, email, phone numbers, etc.

```sql
select TOP 100
	dbo.FakeFirstName(Id) as FirstName, 
	dbo.FakeLastName(Id) as LastName, 
	dbo.FakeCompanyName(OrderId) as CompanyName,  
	dbo.FakeEmailAddress(Id, OrderId) as Email,
	dbo.FakeAddress(OrderId) as Address, 
	dbo.FakeCity(OrderId) as City, 
	dbo.FakePostalCode(OrderId) as PostalCode, 
	dbo.FakePhoneNumber(OrderId) as Phone
FROM Invoices
```

|FirstName|LastName|CompanyName|Email|Address|City|PostalCode|Phone|
|---------|--------|-----------|-----|-------|----|----------|-----|
|Diana|Fritz|Kotova Plc|difritz@kotova-plc.test|29 Lanfranc Place, Lambethtown|Stretford|ST9264|+11 7874 744629|
|Dougie|Gadzhiev|Mironov International|dougie@mironov-international.test|29 Halkin Gate, Walmsley Bay|Torrance|TO9250|+85 9060 60529|
|Emilie|Griffiths|Kozak Co|emilie.griffiths@kozak-co.test|69 Warner Road, Bellendenhampton|Sioux Falls|SI9665|+11 2834 345669|
|Ashley|Carvalho|Busch SRL|ashley.carvalho@busch-srl.test|9 Wager Street, Low Wood|Elkhart|EL9080|+89 2810 10809|
|Aiyla Harris|Anderson|Marx AS|aiyla-harris@marx-as.test|74 Burton Avenue, Ilderton Park|San Bruno|SA4766|+11 7795 956674|
|Jason|Larsson|Gheorghe SRL|jason@gheorghe-srl.test|77 Stukeley Avenue, Herbal East|Stourbridge|ST7738|+80 8728 28377|
|Amara|Baumgartner|Brown|amara.baumgartner@brown.test|13 Notting Street, Leake Cross|Thornton|TH3110|+11 7901 010113|
|Archer|Brun|Komarov & Fonseca Solutions|archer@komarovfonseca-solutions.test|40 Greet Park, Grange South|Altrincham|AL0463|+91 0243 43640|
|Kairo|Magomedov|Persson|kamagomedov@persson.test|1 Little Avenue, Avenue East|Freiburg im Breisgau|FR1002|+94 3272 72001|

### Obfuscating data to remove personally identifiable information (PII)

> ***If you run this anywhere near a production system it will quite literally ruin your life.***
>
> ***So don't do that.***

```sql
UPDATE Customers
	SET FirstName = dbo.FakeFirstName(Id),
	LastName = dbo.FakeLastName(Id), 
	Email = dbo.FakeEmailAddress(Id, CompanyId),
	Phone = dbo.FakePhoneNumber(Id)
	
UPDATE Companies
	SET Name = dbo.FakeCompanyName(Id),
	Address = dbo.FakeAddress(Id), 
	City = dbo.FakeCity(Id), 
	PostalCode = dbo.FakePostalCode(Id), 
	Phone dbo.FakePhoneNumber(OrderId)
```





