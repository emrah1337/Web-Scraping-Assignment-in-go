# Web-Scraping-Assignment-in-go

package main

import (
	"fmt" //standart kütüphaneler
	"log"

	"github.com/PuerkitoBio/goquery" //içeriğe göre erişmek istediğimiz öğeleri seçmemizi sağlar.
)									//go get github.com/PuerkitoBio/goquery komutunu çalıştımamız gerekiyor.

func postScrape() {
	doc, err := goquery.NewDocument("https://codeforces.com/ratings/countries")
	if err != nil {
		log.Fatal(err)
	}

	doc.Find("table .tablesorter-rated-entities-view-table tbody").Each(func(i int, td *goquery.Selection) {
		//tablesorter-rated-entities-view-table ile başlayan satırı bulup devam etmesi için . ile başladım.
		//doc.Find("tbody tr").Each(func(i int, tr *goquery.Selection)
		tr := td.Find("tr").Each(func(k int, tr *goquery.Selection) { // değişken oluşturduk
			//tr.Find("td").Each(func(k int, td *goquery.Selection)
			td := tr.Find("td").Text()
			fmt.Printf("Review %d: %s\n", k, td) // istenilen bilgileri yazdırmaya çalıştım
		}))
	})
}

func main() {
	postScrape()
}
