import pandas
import re
import os

fp = "Wiki_Python.txt"
fp_c = "cleaned Wiki_Python.txt"

if os.path.exists(fp):
    with open(fp, "r", encoding="utf-8") as f:
        wiki = f.read()
else:
    print("Not found!")

# Delete all Wiki links

wiki = re.sub(r"\[/wiki/.*?\]", "", wiki)
                # "\[" - opening bracket
                  # "/wiki/" - beginning of Wikipedia internal link
                        # ".*" - any string with any character except new line
                         # ? - makes "lazy" match - meaning "as little as possible"
                          # "\]" - closing bracket

# lazy match / lazy quantifier
# text = "<tag>one</tag><tag>two</tag>"
# print(re.findall(r"<tag>.*</tag>", text))  -> returns ['<tag>one</tag><tag>two</tag>']
# print(re.findall(r"<tag>.*?</tag>", text)) -> returns ['<tag>one</tag>', '<tag>two</tag>']

# Delete all external links


wiki = re.sub(r"\[[http].*?\]", "", wiki)
wiki = re.sub(r"\[\/[^\]]*\]", "", wiki)

# save cleaned file
with open(fp_c, 'w', encoding='utf-8') as file:
    file.write(wiki)

# All chapters have titles followed by two new lines and the tag [edit ]

# POPULARITY(\n)
# (\n)
# [edit ]

# EXAMPLE 1

print("Example 1:")
print(re.findall("[a-zA-Z]{1,100}\n\n\[edit \]", wiki))

# ['HISTORY\n\n[edit ]', 'FEATURES\n\n[edit ]', 'SEMANTICS\n\n[edit ]', 'INDENTATION\n\n[edit ]', 'FLOW\n\n[edit ]', 
# 'EXPRESSIONS\n\n[edit ]', 'METHODS\n\n[edit ]', 'TYPING\n\n[edit ]', 'OPERATIONS\n\n[edit ]', 'SYNTAX\n\n[edit ]', 
# 'EXAMPLES\n\n[edit ]', 'LIBRARIES\n\n[edit ]', 'ENVIRONMENTS\n\n[edit ]', 'IMPLEMENTATIONS\n\n[edit ]', 'IMPLEMENTATION\n\n[edit ]', 
# 'IMPLEMENTATIONS\n\n[edit ]', 'IMPLEMENTATIONS\n\n[edit ]', 'LANGUAGES\n\n[edit ]', 'PERFORMANCE\n\n[edit ]', 'DEVELOPMENT\n\n[edit ]', 
# 'GENERATORS\n\n[edit ]', 'NAMING\n\n[edit ]', 'POPULARITY\n\n[edit ]', 'USE\n\n[edit ]', 
# 'LIMITATIONS\n\n[edit ]', 'PYTHON\n\n[edit ]', 'ALSO\n\n[edit ]', 'NOTES\n\n[edit ]', 'REFERENCES\n\n[edit ]', 
# 'SOURCES\n\n[edit ]', 'READING\n\n[edit ]', 'LINKS\n\n[edit ]']

# EXAMPLE 2
# We can replace [a-zA-Z]{1,100} with [\w]* to find any letter or digit

print("Example 2:")
print(re.findall("[\w]*\n\n\[edit \]", wiki))

# EXAMPLE 3
# We need to find whole chapter titles, not only last word; they have \n before so we can simple add space to expression

print("Example 3:")
print(re.findall("[\w ]*\n\n\[edit \]", wiki))

# ['HISTORY\n\n[edit ]', 'DESIGN PHILOSOPHY AND FEATURES\n\n[edit ]', 'SYNTAX AND SEMANTICS\n\n[edit ]', 'INDENTATION\n\n[edit ]', 
# 'STATEMENTS AND CONTROL FLOW\n\n[edit ]', 'EXPRESSIONS\n\n[edit ]', 'METHODS\n\n[edit ]', 'TYPING\n\n[edit ]', 'ARITHMETIC OPERATIONS\n\n[edit ]', 
# 'FUNCTION SYNTAX\n\n[edit ]', 'CODE EXAMPLES\n\n[edit ]', 'LIBRARIES\n\n[edit ]', 'DEVELOPMENT ENVIRONMENTS\n\n[edit ]', 'IMPLEMENTATIONS\n\n[edit ]', 
# 'REFERENCE IMPLEMENTATION\n\n[edit ]', 'OTHER IMPLEMENTATIONS\n\n[edit ]', 'UNSUPPORTED IMPLEMENTATIONS\n\n[edit ]', 'COMPILERS TO OTHER LANGUAGES\n\n[edit ]', 
# 'PERFORMANCE\n\n[edit ]', 'LANGUAGE DEVELOPMENT\n\n[edit ]', 'API DOCUMENTATION GENERATORS\n\n[edit ]', 'NAMING\n\n[edit ]', 'POPULARITY\n\n[edit ]', 
# 'TYPES OF USE\n\n[edit ]', 'LIMITATIONS\n\n[edit ]', 'LANGUAGES INFLUENCED BY PYTHON\n\n[edit ]', 'SEE ALSO\n\n[edit ]', 'NOTES\n\n[edit ]', 
# 'REFERENCES\n\n[edit ]', 'SOURCES\n\n[edit ]', 'FURTHER READING\n\n[edit ]', 'EXTERNAL LINKS\n\n[edit ]']

# EXAMPLE 4
# Let's remove "\n\n[edit ]" to keep only titles

print("Example 4:")
for title in re.findall("[\w ]*\n\n\[edit \]", wiki):
    print(re.split("\n\n\[edit \]",title)[0])

# HISTORY
# DESIGN PHILOSOPHY AND FEATURES
# ...
# FURTHER READING
# EXTERNAL LINKS

# EXAMPLE 5
# Assume, there is important data following "\n\n[edit .......]" that we would like to keep while still displaying titles (for example chapter number)

print("Example 5:")
print(re.findall("([\w ]*)(\n\n)(\[edit \])",wiki))

# [('HISTORY', '\n\n', '[edit ]'), 
# ('DESIGN PHILOSOPHY AND FEATURES', '\n\n', '[edit ]'), 
# ...
# ('FURTHER READING', '\n\n', '[edit ]'), 
# ('EXTERNAL LINKS', '\n\n', '[edit ]')]

# EXAMPLE 6
# We can call display specific groups only

print("Example 5:")
for item in re.finditer("([\w ]*)(\n\n)(\[edit \])",wiki): # we use finditer instead findall
    print(item.group(3) + " " + item.group(1))

# [edit ] HISTORY
# [edit ] DESIGN PHILOSOPHY AND FEATURES
# [edit ] SYNTAX AND SEMANTICS
# ...
# [edit ] FURTHER READING
# [edit ] EXTERNAL LINKS

# EXAMPLE 6
# Let's name groups instead call them by position

print("Example 6:")
for item in re.finditer("(?P<title>[\w ]*)(?P<eol>\n\n)(?P<edit>\[edit \])",wiki):
    print(item.groupdict()['title'])

# returns same result as in example 4

# Note: quantifiers
# \w - any word character
# .  - single any character which is not a newline
# \d - any digit

# Look-ahead

# EXAMPLE 7
print("Example 7:")
for item in re.finditer("(?P<title>[\w ]+)(?=\n\n\[edit \])",wiki): # + -> 1 or more
    print (item)

# <re.Match object; span=(6098, 6105), match='HISTORY'>
# <re.Match object; span=(8608, 8638), match='DESIGN PHILOSOPHY AND FEATURES'>

# EXAMPLE 8
print("Example 8:")
for item in re.finditer("(?P<title>[\w ]*)(?=\n\n\[edit \])",wiki): # * -> 0 or more
    print (item)

# <re.Match object; span=(6098, 6105), match='HISTORY'>
# <re.Match object; span=(6105, 6105), match=''>
# <re.Match object; span=(8608, 8638), match='DESIGN PHILOSOPHY AND FEATURES'>
# <re.Match object; span=(8638, 8638), match=''>

# EXAMPLE 9
text = 'Buddhist universities and colleges in the United States\nFrom Wikipedia, the free encyclopedia\n' \
'Jump to navigationJump to search\n\nThis article needs additional citations for verification. Please help ' \
'improve this article by adding citations to reliable sources. Unsourced material may be challenged and removed.\n' \
'Find sources: "Buddhist universities and colleges in the United States" - news · newspapers · books · scholar · ' \
'JSTOR (December 2009) (Learn how and when to remove this template message)\nThere are several Buddhist universities ' \
'in the United States. Some of these have existed for decades and are accredited. Others are relatively new and are ' \
'either in the process of being accredited or else have no formal accreditation. The list includes:\n\nDhammakaya Open ' \
'University - located in Azusa, California, part of the Thai Wat Phra Dhammakaya[1]\nDharmakirti College - located in ' \
'Tucson, Arizona Now called Awam Tibetan Buddhist Institute (http://awaminstitute.org/)\nDharma Realm Buddhist University - ' \
'located in Ukiah, California\nEwam Buddhist Institute - located in Arlee, Montana\nNaropa University is located in ' \
'Boulder, Colorado (Accredited by the Higher Learning Commission)\nInstitute of Buddhist Studies - located in Berkeley, ' \
'California\nMaitripa College - located in Portland, Oregon\nSoka University of America - located in Aliso Viejo, ' \
'California\nUniversity of the West - located in Rosemead, California\nWon Institute of Graduate Studies - located in ' \
'Glenside, Pennsylvania\nReferences[edit]\n^ Banchanon, Phongphiphat (3 February 2015). รู้จัก "เครือข่ายธรรมกาย" [Getting ' \
'to know the Dhammakaya network]. Forbes Thailand (in Thai). Retrieved 11 November 2016.\nExternal links[edit]\nList of ' \
'Buddhist Universities and Colleges in the world'

pattern = """
(?P<title>.*)          # university name
(-\ located\ in\ )     # text to skip
(?P<city>\w*)          # city
(,\ )                  # text to skip
(?P<state>\w*)         # state"""

print("Example 9:")
for item in re.finditer(pattern, text, re.VERBOSE):
    print(item.groupdict())

# {'title': 'Dhammakaya Open University ', 'city': 'Azusa', 'state': 'California'}
# {'title': 'Dharmakirti College ', 'city': 'Tucson', 'state': 'Arizona'}
# {'title': 'Dharma Realm Buddhist University ', 'city': 'Ukiah', 'state': 'California'}
# {'title': 'Ewam Buddhist Institute ', 'city': 'Arlee', 'state': 'Montana'}
# {'title': 'Institute of Buddhist Studies ', 'city': 'Berkeley', 'state': 'California'}
# {'title': 'Maitripa College ', 'city': 'Portland', 'state': 'Oregon'}
# {'title': 'University of the West ', 'city': 'Rosemead', 'state': 'California'}
# {'title': 'Won Institute of Graduate Studies ', 'city': 'Glenside', 'state': 'Pennsylvania'}

# Pull all hashtags from string:
# Each hasttag begins with # and continues until whitespace

pattern ='#[\w\d]*(?=\s)' # ?= in (?=\s) skips that whitespace from being returned

