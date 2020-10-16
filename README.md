[![license](https://img.shields.io/:license-mit-blue.svg)](https://github.com/OzqurYalcin/iys/blob/master/LICENSE.md)

# iys
 An easy-to-use iys.org.tr API with golang

# Installation
```bash
go get github.com/OzqurYalcin/iys
```

# Usage
```go
package main

import (
	"time"

	iys "github.com/OzqurYalcin/iys/src"
)

func main() {
	api := new(iys.API)
	api.Config = iys.Config{
		BaseURL:   "https://api.sandbox.iys.org.tr",
		UserCode:  "",
		BrandCode: "",
		Username:  "",
		Password:  "",
	}
	auth := api.Authorize()
	if auth {
		request := new(iys.Request)
		request.Recipient = "+905055555555"                                     // Alıcı adresi
		request.RecipientType = iys.Individual                                  // Alıcı tipi
		request.ConsentSource = iys.Web                                         // Adres kaynağı
		request.ConsentType = iys.Sms                                           // İzin türü
		request.ConsentStatus = iys.Accept                                      // İşlem türü
		zone, _ := time.LoadLocation("Europe/Istanbul")                         // Saat dilimi
		request.ConsentDate = time.Now().In(zone).Format("2006-01-02 15:04:05") // İzin tarihi
		api.CreateConsent(request)
	}
}
```
