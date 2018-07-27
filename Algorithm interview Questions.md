## Algorithm interview Questions
### 1. Check Prime
**Question**: How would you verify a prime number?
> **Answer**: a prime number is only divisible by itself and 1. So, I will run a while loop and increase by 1.

~~~javascript
function isPrime(n)
{
	var divisor = 2;
	
	while (n > divisor) {
		if ( n % divisor == 0)
			return false;
		else
			divisor++;
	}
	return true
}
~~~
Can you make this better? 
> yes. the divisor are increased 1 at a time. after 3 i can increase by 2. if a number is divisible by any even number, it will be divisible by 2.

~~~javascript
function isPrime(n)
{
  var divisor = 3; 
  var limit = Math.sqrt(n);
  
  // check simple cases
  if (n == 2 || n == 3)
  	return true;
  if (n % 2 == 0)
  	return false;
  	
  while (divisor <= limit) {
  	if (n % divisor == 0 )
  		return false;
  	else
  		divisor += 2;
  }
  return true;
}
~~~

### 2. Prime Factors
**Question**: How could you find all prime factors of a number?
> **Answer**: Run a while loop. start dividing by two and if not divisible increase divider until done.

~~~javascript
function primeFactors(n) {
	var factors = [];
	var divisor = 2;
	
	while (n>2) {
		if (n % divisor == 0) {
			if (!factors.find(divisor) {
				facotrs.push(divisor);
				n = n / divisor;
			}
		}
		else
			divisor++;
	}
	return factors;
}
~~~
What is the run time complexity? Can you make this better?
> This is O(n). You can increase divisor by 2 form divisor = 3. Because, if a number is divisible by any even number it would divisible by 2. Hence, you don't need to divide by even numbers. Besides, you will not have a factor bigger than half of its value.

### 3. Fibonacci
~~~javascript
function fibonacci(n) {
	var fibo = [0, 1];
	
	if (n < 2)
		return 1;
	
	for(var i = 2; i <= n; i++) {
		fibo[i] = fibo[i-1] + fibo[i-2];
	}
	
	return fibo[n];
}
~~~
What is the run time complexity? Can you make it recursive?
> O(n)

~~~javascript
function fibonacci(n) {
	if (n <= 1)
		return n;
	else	
		return fibonacci(n-1) + fibonacci(n-2);
}
~~~
What is the run time complexity?
> O( 2^n )

### 4. Greatest Common Divisor
**Question**: How would you find the greatest common divisor of two numbers?

~~~javascript
function greatCommonDivisor(a, b) {
	var divisor = 2;
	var greatestdivisor = 1;
	
	if (a < 2 || b < 2)
		return 1;
	
	while (a >= divisor && b >= divisor) {
		if (a % divisor == 0 && b % divisor == 0)
			greatestdivisor = divisor;
		divisor++;
	}
	return greatestdivisor;
}
~~~

~~~javascript
function greatCommonDivisor(a, b) {
	if (b == 0)
		return a;
	// a should bigger than b
	return a % b == 0 ? b : greatCommonDivisor(b, a % b);
}
~~~

### 5. remove Duplicate
**Question**: How would you remove duplicate members from an array?
> **Answer**: I will start a while looping and keep an object array. If i find an element for the first time i will set its value as true (that will tell me element added once.). if i find a element in the exists object, i will not insert it into the return array.

~~~javascript
function removeDuplicate(arr) {
	var result = [],
		 exists = {},
		 check;
	
	for (var i = 0; i < arr.length; i++) {
		check = arr[i];
		
		if (!exists[check]) {
			result.push(check);
			exists[check] = true;
		}
	}
	return result
}
~~~

### 6. merge two sorted array
**Question**: How would you merge two sorted array?
> **Answer**: I will keep a pointer for each array.

~~~javascript
function removeDuplicate(arr) {
	var merged = [],
		 aElm = a[0],
		 bElm = b[0],
		 i = 0,
		 j = 0;
	
	if (a.length == 0)	return b;
	if (b.length == 0)	return a;
	
	while (aElm || bElm) {
		if((aElm && !bElm) || aElm < bElm) {
			merged.push(aElm);
			aElm = a[i++]
		}
		else {
			merged.push(bElm);
			bElm = b[j++];
		}
	}
	return merged;
}
~~~

### 7. swap number without temp
**Question**: How would you swap two numbers without using a temporary variable?

~~~javascript
function swapNumb(a, b){
  	console.log('before swap: ','a: ', a, 'b: ', b);
  	b = b - a;
  	a = a + b;
  	b = a - b;
  	console.log('after swap: ','a: ', a, 'b: ', b);  
}
~~~

### 8. string reverse
**Question**: How would you reverse a string in JavaScript?
> **Answer**: I can loop through the string and concatenate letters to a new string

~~~javascript
function reverse(str){
  	var result = '';
  
  	if(!str || typeof str != 'string' || str.length < 2 ) return str;
  
  	for (var i = str.length - 1; i >= 0; i--) {
  		result += str[i];
  	}
  	return result; 
}
~~~
> The run time complexity,  I can loop through half of the index and it will save little bit.

~~~javascript
function reverse(str){
	str = str.split('');
  	var revStr;
  	var len = str.length;
  	var half = Math.floor(len / 2);
  	
  	for (var i = 0; i < half ; i++) {
  		revStr = str[len - i - 1];
  		str[len - i - 1] = str[i];
  		str[i] = revStr;
  	}
  	return str.join(''); 
}
~~~
> That works, but can u do it in a recursive way?

~~~javascript
function reverse(str){
	if (str === "")	return "";
	else
		return reverse(str.substr(1)) + str.charAt(0);
}
~~~
>Can you use any build in method to make it little cleaner?

~~~javascript
function reverse(str){
	if(!str || str.length <2) return str;
	
  	return str.split('').reverse().join('');
}
~~~

### 9. reverse words
**Question**: How would you reverse words in a sentence?
> **Answer**: You have to check for white space and walk through the string. Ask is there could be multiple whitespace.

~~~javascript
function reverseWords(str){
	var rev = [],
		 wordlen = 0;
	
	for (var i = str.length - 1; i >= 0; i--){
		if(str[i] == '' || i == 0) {
			rev.push(str.substr(i, wordlen + 1));
			wordlen = 0;
		}
		else 
			wordlen++;
	}
	return rev.join('');
}
~~~

~~~javascript
function reverseWords(str){
  	return str.split(' ').reverse();
}
~~~

### 10. reverse in place
**Question**: If you have a string like "I am the good boy". How can you generate "I ma eht doog yob"? Please note that the words are in place but reverse.
> **Answer**: To do this, i have to do both string reverse and word reverse.

~~~javascript
function reverseInPlace(str){
  	return str.split(' ').reverse().join(' ').split('').reverse().join('');
}
~~~

### 11. First non repeating char
**Question**: How could you find the first non repeating char in a string?
> Is it very long string or couple hundred? If it is a very long string say a million characters and i want to check whether 26 English characters are repeating. I might check whether all characters are duplicated in every 200 letters (for example) other than looping through the whole string. this will save computation time.

~~~javascript
function firstNonRepeatChar(str){
  	var len = str.length;
  	var char, 
  		 charCount = {};
  	
  	for (var i = 0; i < len; i++) {
  		char = str[i];
  		if (charCount[char]) 
  			charCount[char]++;
  		else
  			charCount[char] = 1;
  	}
  	
  	for (var i in charCount) {
  		if (charCount[i] == 1)
  			return i;
  	}
}
~~~

### 12. remove duplicate char
**Question**: How will you remove duplicate characters from a sting?
> Is it case sensitive. If interviewer says, this is case sensitive then life become easier you. If he says no. you can either use string.toLowercase() to make whole string lower. he might not like it. because return string will not posses the same case.

~~~javascript
function removeDuplicateChar(str){
  	var len = str.length,
  		 char, 
  		 charCount = {},
  		 newsre = [];
  	
  	for (var i = 0; i < len; i++) {
  		char = str[i](.toLowerCase());
  		if (charCount[char]) 
  			charCount[char]++;
  		else
  			charCount[char] = 1;
  	}
  	
  	for (var i in charCount) {
  		if (charCount[i] != 0)
  			newstr.push(i);
  	}
  	return newstr;
}
~~~

### 13. check palindrome
**Question**: How will you verify a word as palindrome?

~~~javascript
function isPalindrome(str){
	var len = str.length;
	for (var i = 0; i < len / 2; i++) {
		if (str[i] != str[len - i - 1])
			return false;
	}
	return true;
}
~~~
or

~~~javascript
function isPalindrome(str){
	return str == str.splot('').reverse().join('');
}
~~~

### 14. random between 5 to 7
**Question**:If you have a function that generate random number between 1 to 5 how could u generate random number 5 to 7 by using that function?

~~~javascript
function rand5(){
   return 1 + Math.random() * 4;
}

function rand7(){
  return 5 + rand5() / 5 * 2;
}
~~~

### 15. missing number
**Question**: from a unsorted array of numbers 1 to 100 excluding one number, how will you find that number.
> **Answer**: You have to act like you are thinking a lot. and then talk about the sum of a linear series of n numbers = n*(n+1)/2

~~~javascript
function missingNumber(arr){
	var n = arr.length + 1,
		 sum = 0,
		 expectSum = n*(n+1)/2;
	
	for (var i in arr) {
		sum += i;
	}
	return expectSum - sum;
}
~~~

### 16. Sum of two
**Question**: From a unsorted array, check whether there are any two numbers that will sum up to a given number?

~~~javascript
function sumFinder(arr, sum){
	var len = arr.length;
	
	for(var i = 0; i < len - 1; i++){
		for(var j = i + 1; j < len; j++){
			if(arr[i] + arr[j] == sum)
				return true;
		}
	}
	return false;
}
~~~
> the time complexity of this function is O(n^2 ).  I can have an object where i will store the difference of sum and element. And then when i get to a new element and if i find the difference in the object, then i have a pair that sums up to the desired sum.

~~~javascript
function sumFinder(arr, sum){
	var len = arr.length,
		 differ = {},
		 delta;
	
	for(var i = 0; i < len; i++){
		delta = sum - arr[i];
		if (diifer[delta])
			return true;
		else
			differ[arr[i]) = true;
	}
	return false;
}
~~~

### 17. Largest Sum
**Question**: How would you find the largest sum of any two elements?

~~~javascript
function topSum(arr, sum){
	var len = arr.length,
		 biggest = arr[0],
		 second = arr[1];
		 
	if (len < 2)	return null;
	
	if (biggest < second) {
		biggest = arr[1];
		second = arr[0];
	}
	
	for(var i = 2; i < len ; i++){
		if (a[i] > biggest) {
			second = biggest;
			biggest = arr[i];
		}
		else if (a[i] > second)
			second = a[i];
	}
	return biggest + second;
}
~~~

### 18. Counting Zeros
**Question**: Count Total number of zeros from 1 up to n?
> **Explanation**: If you have a number 1 to 50 the value is 5. just 50 divided by 10. However, if the value is 100. the value is 11. you will get by 100/10 = 10 and 10/10. Thats how you will get in the more zeros in one number like (100, 200, 1000)

~~~javascript
function countZero(n){
	var count = 0;
	
	while (n > 0) {
		count += Math.floor(n/10);
		n = n/10;
	}
	return count;
}
~~~

### 19. subString
**Question**: How can you match substring of a sting?

~~~javascript
function subStringFinder(str, subStr){
	var idx = 0,
		 i = 0,
		 j = 0;
	
	for (; i < str.length; i++) {
		if (str[i] == subStr[i])
			j++;
		else
			j = 0;
		
		//check string
		if (j == 0)
			idx = i;
		else if (j == subStr.length)
			return idx;
	}
	return -1;
}
~~~

### 20. Permutations
**Question**: How would you create all permutation of a string? 所有字符的全排列
> Idea: Idea is very simple. We will convert the string to an array. from the array we will pick one character and then permute rest of it. After getting the permutation of the rest of the characters, we will concatenate each of them with the character we have picked.

~~~javascript
function permutations(str){
	var arr = str.split(''),
		 len = str.length,
		 perms = [],
		 rest,
		 picked,
		 restPerms,
		 next;
		 
	if (len == 0)		return [str];
	
	for (var i = 0; i < len; i++) {
		rest = Object.create(arr);
		picked = rest.splice(i, 1);
		
		restPerms = permutations(rest.join(''));
		
		for (var j = 0, jLen = restPerms.length; j < jLen; j++) {
			next = picked.concat(restPerms[j]);
			perms.push(next.join(''));
		}
	}
	return perms;
}
~~~








