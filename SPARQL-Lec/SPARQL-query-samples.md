

#  関心のあるリソースのIRIを探す

例）大阪大学のWikidata上でのIRI　　

[http://www.wikidata.org/entity/Q651233](http://www.wikidata.org/entity/Q651233)

---

# 検索例１：主語のみ指定
「大阪大学」を主語（Subject）に含むトリプルの述語（?p）と目的語（?o）を取得する　

```select *
where {
   <http://www.wikidata.org/entity/Q651233> ?p ?o .
}
LIMIT 100
```
---------------

## 検索例1-2：主語のみ指定．その主語が持つプロパティの一覧を取得．

「大阪大学」を主語（Subject）とするトリプルの述語（?p）を取得する（重複除く）

```select distinct ?p
where {
   <http://www.wikidata.org/entity/Q651233> ?p ?o .

}
LIMIT 100
```

　↓　PREFIXを用いた省略表現

```PREFIX wd: <http://www.wikidata.org/entity/>

select distinct ?p
where {
   wd:Q651233 ?p ?o .
}LIMIT 100
```

# 検索例２：主語と述語を指定

## 例2-1）「大阪大学」の「本部所在地」となる目的語（?o）を取得

```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

select distinct ?o
where {
   wd:Q651233 wdt:P159 ?o .
}LIMIT 100
```

## 例2-2） 「大阪大学」のラベルとなる目的語（?o）を取得

```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?o
where {
   wd:Q651233 rdfs:label ?o .
}LIMIT 100
```

## 例2-3)「大阪大学」のラベルとなる目的語（?o）と，その言語種別を取得

```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?o (lang(?o) AS ?ln)
where {
   wd:Q651233 rdfs:label ?o .
}LIMIT 100
```

---
