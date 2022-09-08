
For illustration, here is a list of delete commands, grouped from small to big
objects.  Note that for a single character and a whole line the existing vi
movement commands are used.
	"dl"	delete character (alias: "x")		|dl|
	"diw"	delete inner word			*diw*
	"daw"	delete a word				*daw*
	"diW"	delete inner WORD (see |WORD|)		*diW*
	"daW"	delete a WORD (see |WORD|)		*daW*
	"dgn"   delete the next search pattern match    *dgn*
	"dd"	delete one line				|dd|
	"dis"	delete inner sentence			*dis*
	"das"	delete a sentence			*das*
	"dib"	delete inner '(' ')' block		*dib*
	"dab"	delete a '(' ')' block			*dab*
	"dip"	delete inner paragraph			*dip*
	"dap"	delete a paragraph			*dap*
	"diB"	delete inner '{' '}' block		*diB*
	"daB"	delete a '{' '}' block			*daB*

gx: go to URL

to cut and paste from system clipboard

### How to copy text from vim
```
"+y
```
this sets the selected text to be put in the + register which is the system clipboard

### How to paste stuff from other sources to vim
```
"+p"
```
this pastes any stuff from your system register
Note this seems to work without going through this effort

### How to vim surround

cs"'
replaces "" with '' on something that already surronds a word

ds" will delete parathesis around word

ysiw] will surrond word with a ]
you can use this sentences or paragraphs as well

### More  vim shortcuts
"D" delete up to and including character
"C" delete and go into insert mode
"V" highlight the whole line

