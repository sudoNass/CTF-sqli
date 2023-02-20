## CTF-sqli
### CTF called [Inj3ction Time](https://ctflearn.com/challenge/149) got it from [CTFLearn](https://ctflearn.com).

## CTF SAYS: 
I stumbled upon this website: http://web.ctflearn.com/web8/ and I think they have the flag in their somewhere. UNION might be a helpful command.

well we got the hint we needed which is ``` UNION ``` command.


but first of all we will use ```1 ORDER BY #``` to know how many columns in select query, replace the # by numbers untill you got no results.

![image](https://user-images.githubusercontent.com/107954336/219982939-71a0ea30-eab4-4362-b27c-9d073f485a3f.png)


we got 4 columns so we will use ```union select``` to get them all in the return.

second of all we will test which column can we extract data from by replacing number of column with, ```version()``` or any other command. if one printed the version that means we can use it. 
```null union select 1,version(),3,4```

![image](https://user-images.githubusercontent.com/107954336/219983112-5fa717f7-fe4b-4e9f-9f48-15a66d00e070.png)

we have used "null" so we don't get results from the id and execute the ```union``` command.

we got 1 ,2 & 3 injected so we will use one of them.

third of all we will get the tables name by this injection.

```null union select 1,table_name,3,4 from information_schema.tables```

![image](https://user-images.githubusercontent.com/107954336/219983289-5533df50-f3a5-446d-a03b-3169e9eb7822.png)

we got a lot of results but we are interested in this one.
table name= w0w_y0u_f0und_m3

now we want to get the column name by using this injection.

```null union select 1,column_name,3,4 from information_schema.columns```

![image](https://user-images.githubusercontent.com/107954336/219983752-640f9961-243a-411c-a144-24a2c28a95ef.png)


great,we will take what we want. which is "column name = f0und_m3"

now we have gathered all the pieces we need. we just need to use this information to get what we want.

by using this injection.

```null union select 1,f0und_m3,3,4 from w0w_y0u_f0und_m3```

![image](https://user-images.githubusercontent.com/107954336/219983843-837c3f31-c916-43fc-a2b7-161a7ae1663f.png)


we got the flag.

```abctf{uni0n_1s_4_gr34t_c0mm4nd}```

