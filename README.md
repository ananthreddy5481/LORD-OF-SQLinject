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


