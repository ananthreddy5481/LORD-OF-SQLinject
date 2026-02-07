# LORD-OF-SQLinject

#level-1 :

the site is having an sql injection and wanted any user input for completing the level. so give the "or 1=1-- .

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
%09 -- the ascii form for the tab space.

#level-6 :

in the level the OR and AND are blocked so as we were using the double pipe(||) does not matter for us instead of using the pipe if we use the or then we need to use the || again.

query -- ?pw=' || id='admin'-- 

#level-7 :

this level is combination of lvl 6 and 4, give the ascii charecter of "and" as that is blocked and then procced with the lvl 4 process giving it to the burp suite and brute force that.

and - && - %26%26(ascii)

#level-8 :

this level the id is the parameter and it requires admin as the id.that is blocked using the preg_match.

the preg match is look for the casing and but the sql database is not that means if i give the id=Admin that will bypass because the preg_match is case sensitive and the database is insensitive that returns for the value "admin" from the database and in the if condition that satisfies as the output from the database will be "admin".

#level-9 :

the str_replace function will replace the string in a linear search manner.that is

if i give adadminmin as input and that is searching for admin then

it will select the size of the required string that is 5 here and it will select the first 5 charecters in the input that is "adadm" that is not equal to the required string and repeats the process then in the third case that returns "admin" which is the required one and it will cut that one and concates the first "ad" and the last "min". which is the required parameter value.

level-10 : 

there is a false condition in the second part of the query. 
if the query gives the id=admin and hides the false statement(1=0) in the query then the level will be solved as he is not asking any password.

query : ' or id='admin' -- - 

this makes the condition 1=0 as a part of comment and database does not read that.

level-11 : 

this level needs password but blocks the substr function and also blocks the or,and in the input to by pass that use || and %26%26.

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

here the there is no space between the from and table name which does not make sense in the query structure and the url parameter "shit" is in between them and that is blocked from space,tab space, new line and horizontal tab spaces.

instead of spaces we can use -- %0c - form feed --

%0B - vertical tab spaces -- 

level-15 :


