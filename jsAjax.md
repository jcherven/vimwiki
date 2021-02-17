# AJAX

## the XMLHttpRequest class

an old school way of doing requests. these do not support promises.

```javascript
const myReq = new XMLHttpRequest();

myReq.onLoad = function() {
	const data = JSON.parse(this.responseText);
	console.log(data);
};
myReq.onError = function(err) {
	console.log('Error encountered', err);
};
myReq.open('get', 'https://bandori.party/api/card/1', true);
myReq.setRequestHeader('Accept', ' application/json');
myReq.send();
```


## fetch

Slightly more modern than XMLHttpRequest.

## axios
