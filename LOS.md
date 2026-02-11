# LORD-OF-SQLinjection

#level-1 :

the site is having an sql injection and wanted any user input for completing the level. so give the 'or 1=1-- .

#level-2 :

the site needs to have id=admin and the direct input is taken into the query so can give the parameter id='admin' and comment the rest.
#level-3 :

the site also needs to have id=admin but the id has been set already so use the or id=admin( in hex form because the quotes are banned from using) which makes the server to read the id=guest first and then id=admin and as that is a or function there should be atleast conditon true . 

#level-4 :

give the query as ?pw=' || id='admin' and length(pw) > 7-- 
this for knowing the length of the password. 
?pw' || id='admin' and substr(pw,1,1)='0'-- for this query change the center 1 closing into section sign(§) which is the payload-1 that tells about the position of the charecter in the password that is checking and the "0" that is our payload-2 which is the value of the charecter.
now do brute force that using them.


#level-5 :

here the spaces are blocked so in the url give the tab space(%09) instead of the normal space charecter(%20) because the code blocks the normal space but does not check for the tab space or %09 in the url so we can bypass.
query -- ?pw'%09||%09id='admin'--%09
%09 -- the hex form for the tab space.

#level-6 :

in the level the OR and AND are blocked so as we were using the double pipe(||) does not matter for us instead of using the pipe if we use the "OR" then we need to use the || again.

query -- ?pw=' || id='admin'-- 

#level-7 :

this level is combination of lvl 6 and 4, give the hex charecter of "and" as that is blocked and then procced with the lvl 4 process giving it to the burp suite and brute force that.

and - && - %26%26(ascii)

#level-8 :

this level the id is the parameter and it requires admin as the id.that is blocked using the preg_match.

the preg match is look for the casing and but the sql database is not , that means if i give the id=Admin that will bypass because the preg_match is case sensitive and the database is insensitive that returns for the value "admin" from the database and in the if condition that satisfies as the output from the database will be "admin".

#level-9 :

the str_replace function will replace the string in a linear search manner.that is

if i give "aadmindmin" as input

it will select the size of the required string that is 5 here and it will select the first 5 charecters in the input that is "aadmi" that is not equal to the required string and repeats the process then in the third case that returns "admin" which is the required one and it will cut that one and concates the first "a" and the last "dmin". which is the required parameter value.

level-10 : 

there is a false condition in the second part of the query. 
if the query gives the id=admin and hides the false statement(1=0) in the query then the level will be solved as he is not asking any password.

query : ' or id='admin' -- - 

this makes the condition 1=0 as a part of comment and database does not read that.

level-11 : 

this level needs password but blocks the substr function and also blocks the "or,and" in the input to by pass that use || and %26%26.

for substr replace it with MID function.

mid(searching string , index , jump) -- use this function in burp suite and get the password.

level-12 : 

in this he gave two parameters and for the pw parameter the single quotes are opened but cannot be closed manually so use the second parameter(no) to make the query.

query -- "" || id LIKE "admin" && mid(pw, 1 ,1) LIKE "a"-- - 

give this in burp suite and apply brute force.


level-13 :

LIKE has been blocked here using the preg_match.

INSTR --  can be used instead of like for checking id=admin and for doing brute force while finding the password.

INSTR(id , admin) -- it will check for id=admin in the database and select that user and next apply the brute force for the password.

INSTR - IN STRING (OR) INSTANTIATE STRING 


<img width="633" height="394" alt="Screenshot 2026-02-07 at 10 11 48" src="https://github.com/user-attachments/assets/166aea4c-cc46-4577-ac0d-9f2580dd6248" />

level-14 :

here there is no space between the FROM and table name which does not make sense in the query structure and the url parameter "shit" is in between them and that is blocked from space,tab space, new line and horizontal tab spaces.

instead of spaces we can use -- %0c - form feed --

%0B - vertical tab spaces -- 

level-15 :

it does not have id=guest initially like before levels so we can use the wildcard charecters of sql.

wildcard charecters -- they are used with LIKE statement in the sql query . 

syntax -- pw=a%   ---> this will check any of the element in pw column of database start with "a" or not .
          pw=_a%  ---> this will check any of the element in pw column of the database is "a" or not. 

in this way keep on checking until the admin's pw charecter matches then it will give the id value as admin.

<img width="250" height="89" alt="Screenshot 2026-02-07 at 14 22 09" src="https://github.com/user-attachments/assets/7bb785f6-d138-41fa-ac18-cffe68b1ed90" />

in the first charecters also the admin password will be one of the charecters(brute force charecters) but that may be matched with some other user in the table who is above the admin.

level-16 :

here the level gave two parameters id and pw. both of them are blocked from using single quote(') which will help to close the parameter and generate a new parameter value that does not go in as normal string.

backslash -- this will make the following charecter literal that means that is left behind while preg_match is checking.

if we give / at the id parameter it will make the ending quote of id as normal charecter and the opening quote will not consider this for closing then it will choose the next quote as the closing quote which is the opeing quote of pw . likewise the pw falls into id which makes the new pw that we give is recognised as the active query part.

id=/ pw= or 1=1-- -

level-17 :

addslashes -- this will add slashes infront of predefined( ' , \ , " , NULL CHARECTER)
in the previous lvl we have given backslash to escape the single quote in the query. this time the addslashes is doing that job.

here our goal is to keep the pw parameter value as active to do that if we use single quote the last quote of the pw will have the opening quote of pw to pair makes that inactive.

if i use the backslash it will become (\\). what happens here is the first backslash escapes the first backslash so the closing single quote of the id is not escaped which results the pairing b/w opening quote of id and closing quote of id.

so use the double quote(") or null charecter(%00) which makes the pw parameter value active.

<img width="785" height="411" alt="Screenshot 2026-02-07 at 18 22 34" src="https://github.com/user-attachments/assets/d23cb09b-7adb-4b4f-915a-81f41837d048" />


level-18 : 

<img width="672" height="48" alt="Screenshot 2026-02-08 at 13 34 59" src="https://github.com/user-attachments/assets/0fbe6fd6-a18c-47cc-9580-d777d7efa555" />

here we are leaving the pw parameter value empty that means that is set to zero and we are checking equals to condition that is "empty pw varible is equal to 0 or not"
that is true.

; --> that is used to terminate the statement (to end the statement upto "equals to" statement)

%00 -- null charecter -- the query is most of the times is read upto only null charecter(\n) so the rest is cutoff from the query.

level-19 :

the password cannot be retirved using the brute force.

user defined session varibles -- the session varibles that are created by the user to use in the particular session we can use them to use until the session is expired.

<img width="1124" height="38" alt="Screenshot 2026-02-08 at 16 24 15" src="https://github.com/user-attachments/assets/8aa0b6f3-efe1-435e-a46d-3fbb4eb62449" />

session varible syntax -- @a:=pw -->the @a is the name of the session varible here .

it will store the pw value of the admin.

UNION -- union will combine two select statements 

table 1 : 
<img width="735" height="202" alt="Screenshot 2026-02-08 at 16 33 37" src="https://github.com/user-attachments/assets/4da979f0-a5a0-4fb4-8bdc-24ce7d0145a7" />

table 2 :
<img width="730" height="221" alt="Screenshot 2026-02-08 at 16 34 33" src="https://github.com/user-attachments/assets/c89cbdf8-b27f-4067-8e4a-b9d4f589cbf2" />

AFTER UNION ::
<img width="719" height="258" alt="Screenshot 2026-02-08 at 16 35 16" src="https://github.com/user-attachments/assets/7c58eecf-fc9c-4b1a-af38-5d0f6d23194e" />

in the same way after using the union statement in our case the pw stored in the @pw will become part of the id column and will be returned as the code is returing the result(id) .

<img width="184" height="64" alt="Screenshot 2026-02-08 at 16 37 48" src="https://github.com/user-attachments/assets/daadeb06-4e14-43db-b705-89d1e6396243" />

the password is visible after hello is result of the union which will keep the password in the id column and selects that.


level 20 :

  -- comments the entire text until the line completes.

  \n -- new line charecter -- this will make the text the sql read that it is a new line input.
  use the new liner in hex form.
  
  <img width="926" height="214" alt="Screenshot 2026-02-08 at 17 59 34" src="https://github.com/user-attachments/assets/82d5ab6b-07a1-4d40-acbb-1cef4ea0aacd" />


  level 21 :

  the level does not give any output like before it is used to show hello admin or hello guest.

  but we can do the error based outputs like if the input that we give executed correctly then that will execute another statement which causes the database to produce     an error.

  the query for getting the error based results :
  
  <img width="2730" height="142" alt="image" src="https://github.com/user-attachments/assets/27a313b1-d0dc-4965-9199-7a0a58451124" />

  level 22  :

  instead of if in this we can use the where but this page does not give the error response back like the before page but a blank page means that the database has got an   error input.
  
  <img width="1279" height="64" alt="Screenshot 2026-02-10 at 17 31 17" src="https://github.com/user-attachments/assets/1b8b2ee3-3737-4380-81a7-5380b53dca76" />


  level 23 (hell fire) :
  
<img width="893" height="45" alt="Screenshot 2026-02-11 at 20 16 08" src="https://github.com/user-attachments/assets/e240f3f9-5417-419a-baed-144ab12c1eee" />

here in the if function i am telling the database to execute order value 1 if the condition is true and 3 if the condition is false.

if the condition is true the admin will come in the beggining and if the condition is false the rubiyo id comes at the top.

<img width="294" height="95" alt="Screenshot 2026-02-11 at 20 16 21" src="https://github.com/user-attachments/assets/996f215e-0585-4264-9a07-413ad3ff8ec7" />


**query : ?ORDER=IF(SUBSTR(email,1,1)='a' , 1 , 3 )-- -**

here in this level the real challenge is filtering . in the previous levels we have filtered the correct ouput using the response length but in this case the response length will be almost same and the length will same for incorrect response and correct respose.

to filter we need to use the grep match in the intruder while passing the payloads .

grep match will create another column saying which respose has the specified respose . the grep match searches the html respose for the specified respose .

take anyone of the successfull respose and take the respose like mentioned below ::

successfull response html response:

<img width="771" height="16" alt="Screenshot 2026-02-11 at 20 26 09" src="https://github.com/user-attachments/assets/ea81ba99-3e8c-45a7-9526-d1973031fdd6" />

unsuccessfull response html response:

<img width="772" height="11" alt="Screenshot 2026-02-11 at 20 26 48" src="https://github.com/user-attachments/assets/ae56321f-18ae-47f7-ba0a-ceb339981d04" />

in the successful respone the admin is in the beggining that is in the first row.

<img width="969" height="262" alt="Screenshot 2026-02-11 at 20 28 04" src="https://github.com/user-attachments/assets/49a09d71-9831-4403-afa5-79e210be6ac2" />

the responses get filtered like mentioned below the 1's are with the response given in the grep.

<img width="1345" height="125" alt="Screenshot 2026-02-11 at 20 28 25" src="https://github.com/user-attachments/assets/20653565-97a7-4bcf-a3cd-93a2043b6484" />


  
  
