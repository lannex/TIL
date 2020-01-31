# GORM
ORM을 사용하는 것에 대해 여러 의견이 존재한다. 
ORM만쓰다가 DB를 전혀 모르는 개발자가되느냐 마느냐하는 아직도 다툼이 있는 상황. 
그럼에도 불구하고 ORM은 그 편의성으로 널리 쓰인다.

## Setting
node에서는 sequelize라는 강력한 ORM이 존재하고 Go에서는 GORM이 존재한다. 

ORM이 그렇듯이 약간의 sql지식만이 필요하다. 

'''go
// gorm 설치
go get -u github.com/jinzhu/gorm

// db 설치 - GORM에서 지원하는 것이면 어떤것이든 상관없음
'''

## Usage
'''go

package main

import (
  "github.com/jinzhu/gorm"
  _ "github.com/jinzhu/gorm/dialects/sqlite"
)

type Product struct {
  gorm.Model
  Code string
  Price uint
}

func main() {
  db, err := gorm.Open("sqlite3", "test.db")
  if err != nil {
    panic("failed to connect database")
  }
  defer db.Close()

  // Migrate the schema
  db.AutoMigrate(&Product{})

  // Create
  db.Create(&Product{Code: "L1212", Price: 1000})

  // Read
  var product Product
  db.First(&product, 1) // find product with id 1
  db.First(&product, "code = ?", "L1212") // find product with code l1212

  // Update - update product's price to 2000
  db.Model(&product).Update("Price", 2000)

  // Delete - delete product
  db.Delete(&product)
}
'''

사실상 CRUD 모두다임

ORM이 간단하지만 늘 상황은 다르니 DB공부는 놓지 말아야됨

[gorm](https://gorm.io/)
