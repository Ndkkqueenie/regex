### Identify the old domain
In this section, we will write the body of the function named contains_domain. This function uses regex to identify the domain of the user email addresses in the user_emails.csv file.

The function takes address and domain as parameters, and its primary objective is to check whether an email address belongs to the old domain(abc.edu).

To do this, we will use a regular expression stored in the variable named domain_pattern. This variable will now match email addresses of a particular domain. If the old domain is found, then the function returns true.

```
  domain_pattern = r'[\w\.-]+@'+domain+'$'
  if re.match(domain_pattern, address):
    return True
```
The function contains_domain should now look like this:

```
def contains_domain(address, domain):
  domain_pattern = r'[\w\.-]+@'+domain+'$'
  if re.match(domain_pattern, address):
    return True
  return False
```