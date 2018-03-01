# Ls-Parser
Safe parse Linux Ls Command on Android

In order to access the root directory for android you need to parse the "ls" command.But parsing the "native toolbox ls" command is not reliable and it is not even guranteed that all androids have widely used "ls -l" command.This problem could be solved by installing busybox,but still parsing the output is not considered to be safe. Refer Link for details on "Why not to parse Ls outputs" https://unix.stackexchange.com/questions/128985/why-not-parse-ls


This project will help in safely parsing the "ls" and "find" command.
Following is the step by Tutorial:

1:Download the respective binary of your architecture (from binaries folder) and copy it somewhere in to android's /system/bin directory.Now chmod 555 to make it executable.

2:Ls-Parser supports 3 commands
  
  NOTE: Use Terminal Emulator for Android or RootShell or any other way to execute the commands.Also dont forget to get SuperUser access for restricted directories.
  
  Output for all the 3 commands id of following format
  
    <file_type><"#@$"><permission><"#@$"><item_name><"#@$"><item_size_in_bytes><"#@$"><modified_time_in_long_format><"#@$"><full_path>
    where "#@$" is the delimiter.
    
    <file_type> values:
    1:regular file
    2:directory
    4:symLink pointing to a regular file
    5:symLink pointing to a directory
    
    <permission> is the 9 char (rwxrwxrwx) permission of the item listed.
    
    <modified_time_in_long_format> is the long format time and can be easily coverted to any format of any locale.
    In java it can be done in the following way,
    public String convertTime(long time){
    Date date = new Date(time);
    Format format = new SimpleDateFormat("yyyy MM dd HH:mm:ss");
    return format.format(date);
    }
     
    In case of symlink,<item_size_in_bytes> and <modified_time_in_long_format> gives the details of the item pointed by the symLink.
  
  
 Following are the 3 commands:
  
  COMMAND 1-> to List all the items of directory with detailed info of each item
  
    use command:  myLs 1 "pathToList" 
     
  
  COMMAND 2-> to recursively List all the items of directory with detailed info of each item
  
    use command:  myLs 2 "path_you_want_to_list_recursively" 
    
    
  COMMAND 3-> to search for a file in a directory recursively with detailed info of each item  (DFS Search)
  
    use command:  myLs 3 "path_to_search_in" "name_of_file_to_find" 
    
   
  Here is how to parse the output in Java
      
    String line;//output
    String[] values = line.split("#@$");
    if(values.length!=6)
    {
    //not a valid output,do not parse it
    }
    else
    {
    type=values[0];
    permission=values[1];
    ....
    ....
    path=values[5];
    }
    
    
  

<<<<<<< HEAD

=======
>>>>>>> 0129b16bea81b3ffb65691c72bf003a7d67ff70a
