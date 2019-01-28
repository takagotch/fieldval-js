### fieldval-js
---
https://github.com/FieldVal/fieldval-js

```
npm install
gulp js
mocha test/test

npm install fieldval --save
```

```js
var data = {
  "my_email": "almost@@example.com",
  "my_integer": "clearly not an integer",
  "multiple_of_three" : 8
}
{
  "invalid": {
    "my_email": {
      "error": 107, 
      "error_message": "Invalid email address format/"
    },
    "my_integer": {
      "error_message": "Incorrect field type. Expected number, but received string.",
      "error": 2,
      "expected": "integer",
      "received": "string"
    },
    "multiple_of_three": {
      "error_message": "Not a multiple of three",
      "error": 1000
    }
  },
  "error_message": "One or more errors.",
  "error": 5
}

var validator = new FieldVal(data);
validator.get("my_email", BasicVal.integer(true));
validator.get("my_integer", BasicVal.integer(true));
validator.get("multiple_of_three", BasicVal.integer(true), function(val){
  if(val % 3 !== 0){
    return {
      "error_message": "Not a multiple of three",
      "error": 1000
    }
  }
});
console.log(validator.end());

var FieldVal = require('fieldval');
var BasicVal = FieldVal.BasicVal;
var validator = new FieldVal({
  "my_key": 37
})
var my_key = validator.get("my_key", BasicVal.integer(true), BasicVal.minimum(40));
console.log(validator.end());

var FieldVal = require('fieldval');
var BasicVal = FieldVal.BasicVal;
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(bodyParser.json());
app.post('/', function(req, res){
  var validator = new FieldVal(req.body);
  var id = validator.get("id", BasicVal.number());
  var username = validator.get("username", BasicVal.string());
  var error = validator.end();
  if(error){
    return res.json(error);
  }
  res.json({success:true})
})
app.listen(3000);

function validator_form(data){
  var validator = new FieldVal(data);
  validator.get("name", BasicVal.string(true));
  validator.get("email", BasicVal.email(true));
  return validator.end();
}
var form = new FVForm()
.add_field("name", new FVTextField("Name"))
.add_field("email", new FVTextField("Email"))
.on_submit(funciton(value){
  form.clear_errors();
  var error = validate_form(value);
  if(error){
    form.error(error);
  } else {
    alert(JSON.stringify(value));
  }
})

```

```
// http://www.fieldval.com/docs/fieldval/Examples/Validating%20single%20value
```

