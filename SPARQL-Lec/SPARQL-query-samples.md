

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

## 検索例1-3：PREFIXを用いた省略表現

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

# 検索例3：FILTERによる絞り込み

## 例3-1)「大阪大学」のラベルとなる目的語（?o）から，“日本語のラベルのみ”を取得

```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?o
where { 
   wd:Q651233 rdfs:label ?o . 
   FILTER (lang(?o) = "ja") . 
}LIMIT 100
```

## 例3-2)「大阪大学」のラベルとなる目的語（?o）のうち，“Osaka”という文字列を含むもの取得

```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select distinct ?o
where { 
   wd:Q651233 rdfs:label ?o . 
   FILTER (regex(?o,"Osaka")) . 
}LIMIT 100
```

---

# 検索例4：述語と目的語を指定

## 例）4-1：「国が“日本”と一致する」トリプルの主語（?s）を取得する
```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

select ?s
where { 
 ?s wdt:P17 wd:Q17 . 
}
LIMIT 100
```
## 例）4-2： 「ラベルが“大阪大学”と一致する」トリプルの主語（?s）を取得する
```PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

select ?s
where { 
 ?s rdfs:label "大阪大学"@ja . 
}LIMIT 100
```
## 例）4-3)「大阪大学」のクラス（何のインスタンスか？）を取得する
```PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>

select ?o
where { 
 wd:Q651233  wdt:P31 ?o. 
}
```
## 例4-4)「大学」のインスタンスの一覧を取得する
```PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
select ?s
where { 
  ?s wdt:P31 wd:Q3918. 
}LIMIT 100
```





