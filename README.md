Using ProtoBuffers with Swift and SQL is a total mess. <br/> 
A lot of boilerplate code with hasField() checks. <br/> 
No distinction between 0 and NULL, which is a blasphemy for SQL. 

So here is a little change for protobuf v2 to ease the pain. <br/> 
Optionals without a specified default value will have default default value - NULL.<br/> 

`optional int64 someVar = 1;`<br/> 

will be transformed to 

``` swift
var nullableVar: Int64? {
get {return _nullableVar}
set {_nullableVar = newValue}
}
```

For other cases:<br/> 
`required int64 someVar = 1 [default 0]; //default value will be serialized`<br/> 
`optional int64 someVar = 1 [default 0]; //default value will NOT be serialized`

nothing changes:<br/> 

``` swift
var someVar: Int64 {
get {return _someVar ?? 0}
set {_someVar = newValue}
}
```
