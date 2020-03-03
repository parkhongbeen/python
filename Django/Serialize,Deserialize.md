### Serialize 과정

장고모델 -> Python data type -> Json

serializer = SnippetSerializer(snippet)
	snippet: 		Custom Python object
	serializer:		snippet object를 Python data type으로 변환할 수 있는 Serializer객체
		-> .data (snippet object를 Python data type으로 가져오는 property)





### Deserialize 과정

Json -> Python data type -> 장고모델

Create (data)
Update (instance, data)
