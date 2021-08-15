### Replace the domain name
In this section, we will replace the old domain name with the new one. The second function defined in the script.py file is replace_domain.

The replace_domain function takes in one email address at a time, as well as the email's old domain name and its new domain name. This function's primary objective is to replace the email addresses containing the old domain name with new domain name.

In order to replace the domain name, we will use the regular expression module and make a pattern that identifies sub-strings containing the old domain name within email addresses. We will then store this pattern in a variable called old_domain_pattern. Next, we will use substitution function sub() from re module to replace the old domain name with the new one and return the updated email address.

```
  old_domain_pattern = r'' + old_domain + '$'
  address = re.sub(old_domain_pattern, new_domain, address)
```
The function replace_domain should now look similar to the following:

```
def replace_domain(address, old_domain, new_domain):
  old_domain_pattern = r'' + old_domain + '$'
  address = re.sub(old_domain_pattern, new_domain, address)
  return address
```