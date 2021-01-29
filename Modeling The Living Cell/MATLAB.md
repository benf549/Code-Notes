# Matlab Tutorial

###### From [Tutorial](https://www.youtube.com/watch?v=NSSTkkKRabI)

### Basics

`;` characters mute the output of a statement ot the console.

`=` is the assignment character

`...` can be used to visually break a line across multiple lines





### Terminal I/O

###### Inputting Strings

```matlab
format compact
name = input("what's your name : ", "s");
if ~isempty(name)
	fprintf('Hello %s\n', name);
end
```

The `input()` statement takes the input and the `"s"` argument indicates that you are inputting a string.

The `~` character is the NOT operator in MATLAB

`if` must be terminated with an `end` statement.

`fprintf()` works like printf in other languages.



###### Inputting Vectors

```matlab
vInput = input("Enter a vector : ");
disp(vInput);
```

Here `input` awaits something like `[1 2 3]` which it then prints to the screen with the `disp` function.

### Types

The function `class()` will print the type of the variable passed in. 

- int8
- int16
- int32
- int64
- char
  - Indicated with single quotes
- string
  - Indicated with double quotes
- logical
  - `true` can be used to represent 1
  - `false` can be used to represent 0
- double (default numerical type)
- single
- uint8 (unsigned types inherit all others)

You can typecast by wrapping the value in the thing you want it converted to 

> ex: `int8(16)`

### Printing

```matlab
%prints to terminal. Returns a string
sprintf('5+4 = %d\n', 5 + 4)
sprintf('5+4 = %.2f\n', 5.234 + 4e-2)
```



```matlab
%prints to file (if file specified). Actually prints to the terminal
fprintf('5 + 4 = %d\n', 5 + 4)
```

### Math

```matlab
5 + 4 %add
5 - 4 %subtract
5 * 4 %multiply
5 / 4 %divide
5 ^ 4 %exponentiate
mod(5,4) %modulus
```

Precision is accurate to 15 digits by default (double)

`help elfun` will print all of the elementary math funtions. The most common ones include:

```matlab
abs(-1)
floor(2.45)
ceil(2.45)
round(2.45)
exp(1) %e^x
log(100)
log10(100)
log2(100)
sqrt(100)
deg2rad(90)
```

### Conditional Operators

- ###### Relational Operators
  - `>`
  - `<`
  - `>=`
  - `<=`
  - `==`
  - `~=`

- Logical Operators

  - `||` or
  - `&&` and
  - `~` not

###### If Else Statements

```matlab
age = 12;
if age >= 5 && age <= 6
	disp('Your''re in Kindergarten')
elseif age >= 7 && age <= 13
	disp('Your''re in middle school)
elseif age >= 14 && age <= 18
	disp('Your''re in high school')
else
	disp('Stay Home')
end
```

###### Switch Statement Control Flow

```matlab
age = 12;
switch age
	case 5
		disp("Your're in kindergarten")
	case num2cell(6:13)
		disp("middle school")
	case {14, 15, 16, 17, 18}
		disp("high school")
	otherwise
		disp("stay home")
end
```

`num2cell(6:13)` converts the numeric array `6:13` to a cell array.

### Vectors

Can be row or column vectors

```matlab
vt1 = [5 3 2 1]
vL = length(vt1)
vt1 = sort(vt1, 'descend') %default is ascending
vt2 = 5:10
vt3 = 2:2:10 %from 2 to 10 in steps of 2 (middle)
vt4 = [vt1 vt2]
vt4(1) %vectors are 1 indexed
vt4(end) %end gives last element
vt4(1) = 12
vt4(11) = 33 %zeros added in between if not end+1
vt4(1:4)
vt4([2 4 6]) %choose just 2, 4, 6th item

vt5 = [2;3;4] %The semicolons make a column vector
vt6 = [1 2 3]

vtMult = vt5 * vt6 %matrix multiplication.

vt7 = [4 5 6]
vtDotP = vt6 * vt7' %dot product
vtDotP2 = dot(vt6, vt7) %dot product

vtElementWise = vt6.*vt7 %elementwise multiplication

vt8 = linspace(1,20,4) %same as numpy (start, end, step)
vt9 = logspace(1,3,3)
```

Vectors in MATLAB are **<u>1 indexed</u>** unlike other languages.

When you assign an index to a value that is larger than the current largest index, the intermediate values get filled with zeros.

**Transposing** a vector is done by simply adding a tickmark such as `vt7'`

### Matrices

```matlab
m1 = [2 3 4; 4 6 8]
mNRV = length(m1) % Number of rows
mNV = numel(m1) % total number of values
mS = size(m1) % row x col
[nRows, nCols] = size(m1)

%indexing
m1(1,1)
m1(1,:)
m1(:,1)
m1(end,end) = 5
m1(:,2) = [] %deletes second column
```



###### Random Values

```matlab
m2 = randi([10, 20], 2,3) %generate random ints (between[], shape)
```

### Looping

```matlab
for i = 10:-1:0
	disp(i)
end

m4 = [2 3 4; 4 6 8]
for i = 1:2
	for j = 1:3
		disp(m4(i,j))
	end
end

IVect = [6 7 8]
for i = 1:length(IVect)
	disp(IVect(i))
end

% while loops
i = 1;
while i < 20
	if (mod(i, 2)) == 0
		disp(i)
		i = i + 1;
		continue
	end
	i = i + 1;
	if i >= 10 %leaves loop prematurely
		break
	end
end
```

### Matrix Functions

```matlab
m3 = [2 3 4; 5 6 7; 8 9 10]
m4 = [1:3; 4:6]
m5 = [2:4; 5:7]

m4 + m5
m4 .* m5

%functions applied element wise
sqrt(m3)
m3 = m3 * 2 %mult each value by 2
sum (m3) %sums all columns

%matrix multiplication
m6 = [1 2 3; 4 5 6]
m7 = [1 1 1 1; 2 2 2 2; 3 3 3 3]
m8 = m6 * m7

%boolean matrix
gT3M = m4 > 3
sum(gT3M, 'all') % how many are equal to 3

isequal(m4, m5)
find(m3 > 4)

prod(m3) %multiply columns

cumsum(m3) %each row is summed consecutively
cumprod(m3) %each row multiplied consecutively

fliplr(m3) %flip first column with last
flipud(m3) %flip horizontally
rot90(m3) %rotate matrix 90
rot90(m3, 2) %rotate 180deg

reshape(m3, 2, 6) %reshape matrix
repmat(m3, 2, 1) %duplicate matrix into new matrix of shape 2x1
replelem(m3, 2, 1) %duplicates elements into new matrix where you have two rows for each value. 
```

### Cell Arrays

```matlab
cA1 = {'Doug Smith', 34, [25 8 9]}
cA2 = cell(5)
cA1{1} %index first
cA1{3}(2) %index third and index vector
cA1{4} = 'Patty Smith'
length(cA1)
cA1{4} = [] %delete last index
for i in i:length(cA1)
	disp(cA1{i})
end

cA3 = {'Doug' 'Patty'}
nameMat = char(cA3) %converts cell array to character array
cA4 = cellstr(nameMat) %convert character arrays to cell arrays

```

### Character Arrays

Character Arrays are just vectors of characters. 

```matlab
str1 = 'I am a chararray'
length(str1)
str(1)
str1(3:4)
str = strcat(str1, ' that''s longer')
strfind(str2, 'a')
strrep(str2, 'longer', 'bigger') %replace 'longer' with 'bigger'
strArray = strsplit(str1, ' ') %split by ' ' into cell array
class(strArray)
strArray(1)

nStr = int2str(99) %convert int to character array
nStr2 = num2str(3.14) %convert float to character array
strcmp(str1, str2) %test if strings are equal
isletter('num 2') %returns logical array of whether each index is letter.
isstrprop('word2', 'alpha') %same checks for letters(alpha) or letters and numbers (alphanum)
ischar('some words 2')
sort(str1)
strtrim(str1) %remove white space from beginning and end
lower(str1)
upper(str1)
```



### Structures

```matlab
dougSmith = struct('name', 'Doug Smith', ...
	'age', 34, 'purchases', [12 23]) 
disp(dougSmith.age)
dougSmith.wife = 'Patty Smith' %can add attributes after creation
dougSmith = rmfield(dougSmith, 'wife') %remove attributes after creation
isfield(dougSmith, 'wife') %test if attribute defined
fieldnames(dougSmith) %get all the field names
customers(1) = dougSmith; %add them to arrays
sallSmith = struct('name', 'Sally Smith', ...
	'age', 34, 'purchases', [12 23])
customers(2) = sallSmith;

disp(customers(2).name) %select attributes from within arrays
```

Structures are like objects in other languages. An attribute of the object can be selected with the `obj.attribute` syntax. 

### Tables

Labelled rows of data in a table format. 

```matlab
name = {'Jim'; 'Pam'; 'Dwight'}
age = [28;27;31];
salary = [35000; 26000; 75000];
id = {'1';'2';'3'}

employees = table(name, age, salary, ...
	'RowName', id)
meanSalary(mean(employees.salary))
employees.vDays = [10, 14, 16]; %add a table row
employees({'1', '2'}, :)
employees(ismember(employees.name, ...
	{'Jim', 'Dwight'}), :)
```

Running `help table` gives an overview of all the things you can do with a table. 

### File I/O

Saving Matrices and Variables

```matlab
randM = randi([10,50], 8)
save sampdata1.dat randM -ascii %creates/overwrites .dat file
load sampdata1.dat
disp sampdata1
type sampdata1.dat

%saves all variables used
save myData1
load myData1
who
v4 = 123
save -append myData1 v4 %append saved data with v4
```

### Functions

```matlab
cylinderCol(20,30)

%functions have to go below where they're called
function vol = cylinderVol(radius, height)
	vol = pi * radius^2 * height
end
```

Defining a function in this way is as follows `function return_value = name(params)`.

###### Variable Scope

Variables defined within a function are local and do not have access to external variables with the same name. 

```matlab
changeMe = 5
changeVal()
disp(changeMe)
function changeVal()
	changeMe = 10
	class(changeMe)
end
```

###### Return Number

```matlab
getRandomNum()

function randNum = getRandomNum()
	randNum = randi([1,100])
end
```

###### Returning More than One Value

```matlab
[coneVol, cylVol] = getVols(10, 20)

function [coneVol, cylVol] = getVols(radius, height)
	cylVol = pi * radius^2 * height
	coneVol = 1/3 * cylVol
end
```

###### Accept Variable Number of Arguments

```matlab
theSum = getSum(1,2,3,4)

function sum = getSum(varargin)
	sum = 0;
    for k = 1:length(varargin)
        sum = sum + varargin{k}(1);
    end
end
```

###### Return a Variable Number of Values

```matlab
listOfNums = getNumbers(10)

function [varargout] = getNumbers(howMany)
	for k = 1:howMany
		varargout{1}(k) = k;
	end
end
```

###### Anonymous Functions (lambda functions)

```matlab
cubeVol = @ (l,w,h) l * w * h
cV = cubeVol(2,2,2)
```

###### Passing a Function to Another Function

```matlab
mult3 = @ (x) x * 3
sol = doMath(mult3, 4)

function sol = doMath(func, num)
	sol = func(num)
end
```

###### Returning a Function from Another Function

```matlab
mult4 = doMath2(4);
sol2 = mult4(5)

function func = doMath2(num)
	func = @(x) x*num;
end
```

###### Execute Code Saved In A String

```matlab
toExecute = sprintf("total = %d + %d", 5, 4)
eval(toExecute)
```

###### Recursion

```matlab
factorial(4)
function val = factorial(num)
	if num <= 1
		val = 1;
	else
		val = num * factorial(num - 1);
	end
end
```

### Classes

A class must be in its own file called `Name.m` where Name is the name of the class being defined.  

```matlab
classdef Shape
	properties
		height;
		width;
	end
	
	%declare static methods first
	methods(Static)
		function out = setGetNumShapes(data)
			persistent Var;
			if isempty(Var)
				Var = 0;
			end
			if nargin
				Var = Var + data;
			end
			out = Var;
		end
	end
	
	methods
		%Constructor
		function obj = Shape(height, width)
			obj.height = height;
			obj.width = width;
			obj.setGetNumShapes(1);
		end
		% Overload the default disp function
		function disp(obj)
			fprintf('Height : %.2f / Width : %.2f\n', ...
            	obj.height, obj.width);
        end
        %calculate area
        function area = getArea(obj)
        	area = obj.height * obj.width;
        end
        %Overload greater than operator
        function tf = gt(obja, objb)
        	tf = obja.getArea > objb.getArea;
        end
 	end
end
```

Then from other script files, the constructor can be called like this:

```matlab
a = Shape(10, 10)
disp(a)
b = Shape(10, 11)
disp(b)
b > a

a.getArea
Shape.setGetNumShapes
```

###### Inheritance

```matlab
classdef Trapezoid < Shape %Inherits from Shape
    properties
        width2;
    end
    
    methods
        function obj = Trapezoid(height, width, width2)
            obj @ Shape(height, width);
            obj.width2 = width2;
            
        end
        
        function disp(obj)
			fprintf('Height : %.2f / Width : %.2f / Width2 : %.2f\n', ...
            	obj.height, obj.width, obj.width2);
        end
        function area = getArea(obj)
        	area = (obj.height/2) * (obj.width + obj.width2);
        end
    end
end
```

### Plotting

###### Scatter

```matlab
xVals = 1:5
yVals = [2 4 8 5 9]
yVals2 = [1 5 7 6 8]

figure(1)
plot(xVals, yVals, 'go', 'LineWidth', 2) %help plot
hold on
plot(xVals, yVals2, 'k*', 'LineWidth', 2)
legend('yVals', 'yVals2')
grid on
xlabel('Days')
ylabel('Money')
title('Money per Day')
```

###### Bar

```matlab
figure(2)
bar(xVals, yVals, 'r')
```

