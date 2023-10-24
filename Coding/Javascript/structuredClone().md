This is a built-in function of Javascript that for some reason is not very known

It does a deep copy of a certain object. It's the alternative to doing: 

```javascript
const clonedObject = JSON.parse(JSON.stringify(object))
```

But that solution is very hacky and I don't like it 
