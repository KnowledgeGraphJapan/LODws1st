#  関心のあるリソースのIRIを探す
例）大阪大学のWikidata上でのIRI　　
  [http://www.wikidata.org/entity/Q651233](http://www.wikidata.org/entity/Q651233)
---

#  検索例１：主語のみ指定
「大阪大学」を主語（Subject）に含むトリプルの述語（?p）と目的語（?o）を取得する　

```select *
where {
   <http://www.wikidata.org/entity/Q651233> ?p ?o .
}
LIMIT 100
```
---------------
