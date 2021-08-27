---
layout: post
title:  "XML vs JSON vs YAML"
subtitle:   "XML vs JSON vs YAML"
categories: java&spring
tags: Spring   
comments: true
---


# XML  vs  JSON  vs   YAML

---

안녕하세요! 프로그램을 개발하다 보면 .xml, .yml, .json 과 같은 파일들을 많이 발견할 수 있습니다. 그래서 오늘은 **XML과 YAML(yml), Json**이 각각 사용되는 곳을 알아보고 마지막으로 각각의 사용 방법에 대해 알아보도록 하겠습니다.

## 1. XML

XML은 **데이터를 저장하고 전달할 목적**으로 만들어졌으며, 저장되는 **데이터의 구조**를 기술하기 위한 언어입니다. XML은 EXtensible Markup Language의 약자로, 수많은 응용 분야에서 데이터를 저장하고 전달하는 중요한 역할을 맡고 있습니다.

우리는 기본적으로 Markup Language로 HTML을 떠올릴수 있습니다. XML의 구조는 HTML과 매우 유사하지만 큰 차이점이 존재합니다. 예를 들면 HTML에서는 미리 약속된 태그들만 사용할수 있습니다.(ex. \<a\> , \<p\>) 하지만 XML에서는 사용자가 태그를 임의로 만들수 있습니다. XML은 트리계층 구조를 가지고 있고 루트 요소부터 시작해 여러 개의 자식을 계층적으로 포함하게 됩니다.

XML은 문법적인 오류가 발생해도 각각 태그로 구분되어 있기 때문에 다른 태그들은 컴퓨터가 읽을 수 있습니다. 따라서 안정성을 요구하는 곳에서 XML을 사용하면 좋습니다. 

```xml
<?xml version="1.0"?>
<EmpRecord>
<Employee id="emp01">
<name>Alex</name>
<job>Developer</job>
<skills>python, C/C++, paskal</skills>
</Employee>
 
<Employee id="emp02">
<name>Bob</name>
<job>Tester</job>
<skills>lips, forton, REST APIs</skills>
</Employee>
 
</EmpRecord>
```



## 2. JSON

JSON은 자바스크립트의 객체 표기법으로부터 파생된 부분 집합입니다. 예전에는 자바스크립트에서 많이 사용되었지만 최근에는 다양한 프로그래밍 언어에서 사용됩니다. 일반적으로 서버와의 통신 규악인 REST API를 사용할 때 가장 많이 사용되어, 최근에는 XML보다 JSON 형식이 채택되고 있습니다. 

JSON은 문법적인 오류에 취약하기 때문에 문법적인 오류가 하나라도 발생하면 문서 전체가 해석 불가능한 상태가 됩니다. 따라서 가벼움을 중시하는 곳에서는 JSON을 사용하면 좋습니다. 위의 XML을 JSON으로 변환하면 다음과 같습니다.

```json
{
	"EmpRecord": {
		"Employee": [
			{
				"-id": "emp01",
				"name": "Alex",
				"job": "Developer",
				"skills": "python, C/C++, paskal"
			},
			{
				"-id": "emp02",
				"name": "Bob",
				"job": "Tester",
				"skills": "lips, forton, REST APIs"
			}
		]
	}
}
```

## 3. YAML

YAML은 *"**YAML Aint Markup Language**"*로 *"**마크업 언어가 아니다**"*로 정의가 되어있습니다. 또한 데이터의 구조를 표현하기 위해 들여쓰기를 사용합니다. 통해  또한 JSON과 비슷하게 사람이 읽기 쉬운 형태의 데이터 표현 형식입니다. YAML은 XML과 문법적으로 유사합니다. YAML에서도 주석이 사용 가능하고 개행, 공백으로 블록을 인식합니다. 쓰고 있는 사람의 편의를 우선시하기 때문에 docker compose나 spring의 설정 파일에 자주 사용하게 됩니다. 위의 JSON을 YAML으로 변환하면 다음과 같습니다.

```yaml
 # Employee records
 
 - Employee one:
    name: Alex
    job: Developer
    skills:
        - python
        - C/C++
        - pascal
 		
 - Employee two:
    name: Bob
    job: Tester
    skills:
        - lips
        - forton
        - REST APIs
 ```

---

## 요약

오늘은 XML, JSON, YAML에 대해 알아보았습니다. 이 세개 모두 데이터 직렬화를 위한 표준 규약으로 따로 정해진 규칙 없이 상황에 맞게 적절히 사용하면 좋을것 같습니다. 

