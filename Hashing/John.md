# John
#### Using Single Crack Mode

To use single crack mode, we use roughly the same syntax that we've used to so far, for example if we wanted to crack the password of the user named "Mike", using single mode, we'd use:  
 

`john --single --format=[format] [path to file]`

`--single` - This flag lets john know you want to use the single hash cracking mode.

**Example Usage:**

john --single --format=raw-sha256 hashes.txt

**A Note on File Formats in Single Crack Mode:**

If you're cracking hashes in single crack mode, you need to change the file format that you're feeding john for it to understand what data to create a wordlist from. You do this by prepending the hash with the username that the hash belongs to, so according to the above example- we would change the file hashes.txt

**From:**   
 

1efee03cdcb96d90ad48ccc7b8666033

**To**

mike:1efee03cdcb96d90ad48ccc7b8666033

#### How to create Custom Rules

Custom rules are defined in the `john.conf` file, usually located in `/etc/john/john.conf`

The first line:

`[List.Rules:THMRules]` - Is used to define the name of your rule, this is what you will use to call your custom rule as a John argument.

We then use a regex style pattern match to define where in the word will be modified, again- we will only cover the basic and most common modifiers here:

`Az` - Takes the word and appends it with the characters you define   
 

`A0` - Takes the word and prepends it with the characters you define  
 

`c` - Capitalises the character positionally

`[List.Rules:PoloPassword]`

`cAz"[0-9] [!£$%@]"`

In order to:

Capitalise the first  letter - `c`

Append to the end of the word - `Az`

A number in the range 0-9 - `[0-9]`

Followed by a symbol that is one of `[!£$%@]`

`john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]`