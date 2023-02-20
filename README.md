[![license](https://img.shields.io/:license-mit-blue.svg)](https://github.com/ozgur-yalcin/iys/blob/master/LICENSE.md)
[![documentation](https://pkg.go.dev/badge/github.com/ozgur-yalcin/iys)](https://pkg.go.dev/github.com/ozgur-yalcin/iys/src)

# iys
iys.org.tr (İleti Yönetim Sistemi) Golang API

# Installation
```bash
go get github.com/ozgur-yalcin/iys
```

# Mail gönderim izni
```go
package main

import (
	"time"

	iys "github.com/ozgur-yalcin/iys/src"
)

func main() {
	api := new(iys.API)
	api.Config = iys.Config{
		BaseURL:   "https://api.sandbox.iys.org.tr",
		UserCode:  "123456",
		BrandCode: "123456",
		Username:  "user@example.com",
		Password:  "pass",
	}
	auth := api.Authorize()
	if auth {
		request := new(iys.Request)
		request.Recipient = "info@test.com"                                     // Alıcı adresi
		request.RecipientType = iys.Individual                                  // Alıcı türü
		request.ConsentSource = iys.Web                                         // Adres kaynağı
		request.ConsentType = iys.Mail                                          // İzin türü
		request.ConsentStatus = iys.Accept                                      // İşlem türü
		zone, _ := time.LoadLocation("Europe/Istanbul")                         // Saat dilimi
		request.ConsentDate = time.Now().In(zone).Format("2006-01-02 15:04:05") // İzin tarihi
		api.CreateConsent(request)
	}
}
```

# Sms gönderim izni
```go
package main

import (
	"time"

	iys "github.com/ozgur-yalcin/iys/src"
)

func main() {
	api := new(iys.API)
	api.Config = iys.Config{
		BaseURL:   "https://api.sandbox.iys.org.tr",
		UserCode:  "123456",
		BrandCode: "123456",
		Username:  "user@example.com",
		Password:  "pass",
	}
	auth := api.Authorize()
	if auth {
		request := new(iys.Request)
		request.Recipient = "+905055555555"                                     // Alıcı adresi
		request.RecipientType = iys.Individual                                  // Alıcı türü
		request.ConsentSource = iys.Web                                         // Adres kaynağı
		request.ConsentType = iys.Sms                                           // İzin türü
		request.ConsentStatus = iys.Accept                                      // İşlem türü
		zone, _ := time.LoadLocation("Europe/Istanbul")                         // Saat dilimi
		request.ConsentDate = time.Now().In(zone).Format("2006-01-02 15:04:05") // İzin tarihi
		api.CreateConsent(request)
	}
}
```

# Telefon arama izni
```go
package main

import (
	"time"

	iys "github.com/ozgur-yalcin/iys/src"
)

func main() {
	api := new(iys.API)
	api.Config = iys.Config{
		BaseURL:   "https://api.sandbox.iys.org.tr",
		UserCode:  "123456",
		BrandCode: "123456",
		Username:  "user@example.com",
		Password:  "pass",
	}
	auth := api.Authorize()
	if auth {
		request := new(iys.Request)
		request.Recipient = "+905055555555"                                     // Alıcı adresi
		request.RecipientType = iys.Individual                                  // Alıcı türü
		request.ConsentSource = iys.Web                                         // Adres kaynağı
		request.ConsentType = iys.Call                                          // İzin türü
		request.ConsentStatus = iys.Accept                                      // İşlem türü
		zone, _ := time.LoadLocation("Europe/Istanbul")                         // Saat dilimi
		request.ConsentDate = time.Now().In(zone).Format("2006-01-02 15:04:05") // İzin tarihi
		api.CreateConsent(request)
	}
}
```