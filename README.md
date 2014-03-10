AUEB_POS_tagger
===============

This file accompanies the software of AUEB’s Greek part-of-speech (POS) tagger 
version 2 alpha. Unlike the k-NN-based version 1.0, which is still available 
(see http://nlp.cs.aueb.gr/software/), this version uses Stanford's Maximum 
Entropy Classifier (see http://nlp.stanford.edu/software/classifier.shtml) 
and performs better. This version, however, does not yet provide a graphical
user interface, nor active learning facilities, unlike version 1.0, but it
provides an application programming interface (API), which was missing in the 
previous version. Like the previous version, the new version supports two
tagsets, a coarse (small) one (with tags for verb, noun, article, etc.) and a 
fine (large) one (with tags showing, for example, also the gender, number, and 
case of each noun occurrence, the tense, number, person etc. of verb occurrences 
etc). The tags of the two tagsets are listed in coarse_tagset.txt and 
fine_tagset.txt.

This version of the tagger was developed during Evangelia Koleli's BSc thesis 
in the Department of Informatics, Athens University of Economics and Business
(AUEB), Greece, 2011 (see http://nlp.cs.aueb.gr/theses.html). It is based on 
previous versions developed by Prodromos Malakasiotis, Ioannis Chronakis, 
and Costas Pappas. 

Copyright notes: 
================
The software of AUEB's Greek POS tagger version 2 alpha is released under the 
GNU General Public 
License (version 3.0); please consult the file 
gpl-3.0.html for more information. THE TAGGER IS A RESEARCH PROTOTYPE AND IT 
IS PROVIDED WITH ABSOLUTELY NO GUARANTEE AND ABSOLUTELY NO SUPPORT! However, 
you may e-mail bug reports to evakoleli@gmail.com.

The distribution of AUEB's Greek POS tagger version 2 alpha includes the 
software of Stanford's Maximum Entropy Classifier (version 2.0). The following 
is copied verbatim from Stanford's Classifier web page. Please make sure that 
you comply with the restrictions of Stanford Classifier's license.

"The Stanford Classifier is available for download, licensed under the GNU 
General Public License (v2 or later). Source is included. The Stanford 
Classifier code is dual licensed (in a similar manner to MySQL, etc.). Open 
source licensing is under the full GPL, which allows its use for research 
purposes, free software projects, etc. For distributors of proprietary 
software, commercial licensing with a ready-to-sign agreement is available." 


Installation:
=============
In order to use this software correctly follow the instructions below:

1. Move the entire (unzipped) directory "AUEB_POS_tagger_2alpha" to the 
directory that you prefer (e.g., to "c:\mydir").
2. Add "...\AUEB_POS_tagger_2alpha\bin\POStagger.jar" and 
"...\AUEB_POS_tagger_2alpha\bin\lib\stanford-classifier.jar" (e.g., 
"c:\mydir\AUEB_POS_tagger_2alpha\bin\POStagger.jar") to your CLASSPATH
system variable. 


Using the API:
==============

Only three classes have methods with public access. The public methods of 
the three classes are documented below. See the "javadoc" directory for
further documentation.

1. Public methods of class gr.aueb.cs.nlp.postagger.SmallSetFunctions:
---------------------------------------------------------------------- 

1.1 Method smallSetClassifyFile(String):
		
DESCRIPTION:
A static method that classifies (tags) every token (word, symbol etc.) 
of a text file (in UTF-8 encoding) using the coarse tagset. All the 
tokens of the file must be separated by whitespace characters (e.g. 
" äõíÜìåùí , äÞëùóå êÜôïéêïò ôçò ðüëçò óôï ðñáêôïñåßï Reuters . ").

INPUT: String - the location of the text file.
OUTPUT: List <WordWithCategory> - a list of every token of the file with 
its guessed category (tag). 
		
EXAMPLE:
List<WordWithCategory> list;
list = SmallSetFunctions.smallSetClassifyFile("my_file.txt");
for (int i=0;i<list.size();i++){
   System.out.println(list.get(i).toString());
}
		    
1.2 Method smallSetClassifyString(String):
		
DESCRIPTION:
A static method that classifies (tags) every token of a string using the
coarse tagset. All the tokens of the string must be separated by 
whitespace characters.

INPUT: String - the string containing the tokens.
OUTPUT: List <WordWithCategory> - a list of every token of the string 
with its guessed category (tag). 
		
EXAMPLE: 
List<WordWithCategory> list;
list = SmallSetFunctions.smallSetClassifyString(" ÐñùôïöáíÞò 
   åêôñï÷éáóìüò ôïõ ðñïûðïëïãéóìïý êáé « ìáýñç » ôñýðá Üíù ôïõ 1 
   äéó. . Ï õðïõñãüò Ïéêïíïìéêþí ðáñáäÝ÷åôáé üôé õðÜñ÷åé óôÝñçóç 
   åóüäùí êáé ðñïåéäïðïéåß üôé åÜí ôï ðñüâëçìá äå ëõèåß ìÝóá óôïõò 
   åðüìåíïõò ìÞíåò , ôüôå ç êõâÝñíçóç èá ðñï÷ùñÞóåé óôç ëÞøç íÝùí 
   ìÝôñùí . ");
for (int i=0;i<list.size();i++){
   System.out.println(list.get(i).toString());
}

EXAMPLE OUTPUT:
ÐñùôïöáíÞò noun
åêôñï÷éáóìüò noun
ôïõ article
ðñïûðïëïãéóìïý adjective
êáé conjunction
« punctuation
ìáýñç adjective
» punctuation
ôñýðá adjective
Üíù adverb
ôïõ article
1 numeral
äéó. other
. punctuation
Ï article
õðïõñãüò noun
Ïéêïíïìéêþí noun
ðáñáäÝ÷åôáé verb
üôé conjunction
õðÜñ÷åé verb
óôÝñçóç noun
åóüäùí adjective
êáé conjunction
ðñïåéäïðïéåß verb
üôé conjunction
åÜí other
ôï article
ðñüâëçìá noun
äå particle
ëõèåß verb
ìÝóá adverb
óôïõò article
åðüìåíïõò adjective
ìÞíåò noun
, punctuation
ôüôå adverb
ç article
êõâÝñíçóç noun
èá particle
ðñï÷ùñÞóåé verb
óôç article
ëÞøç noun
íÝùí adjective
ìÝôñùí noun
. punctuation
    
1.3 Method smallSetEvaluateFile(String):
		
DESCRIPTION:
A static method that computes the tagger's accuracy, given a file (in UTF-8 
encoding) containing a sequence of tokens and their correct coarse categories 
(tags). The file must contain one line for each token, and each line must 
contain the token followed by the correct tag, separated by a space, as in 
the example output of the previous method. 

INPUT: String - the location of the file.
OUTPUT: double - the tagger's accuracy on the tokens of the input file. 

EXAMPLE:
System.out.println(BigSetFunctions.bigSetEvaluateFile("my_test_file.txt"));
					
1.4 Method smallSetTrainOtherClassifier(String):
		
DESCRIPTION:
A static method that trains the tagger on a file (in UTF-8 encoding) 
containing a sequence of tokens and their correct coarse categories (tags). 
The file must be in the same format as the example output of method 1.2.

INPUT: String - the location of the file.

EXAMPLE:
SmallSetFunctions.smallSetTrainOtherClassifier("my_train_file.txt");
			
					
2. Public methods of class gr.aueb.cs.nlp.postagger.BigSetFunctions:
--------------------------------------------------------------------

2.1 Method bigSetClassifyFile(String):
		
DESCRIPTION:
A static method that classifies (tags) every token of a text file 
(in UTF-8 encoding) using the fine tagset. All the tokens of the 
file must be separated by whitespace characters.

INPUT: String - the location of the text file.
OUTPUT: List <WordWithCategory> - a list of every token of the 
file with its guessed category (tag).
		
EXAMPLE: 
List<WordWithCategory> list;
list = BigSetFunctions.bigSetClassifyFile("my_file.txt");
for (int i=0;i<list.size();i++){
   System.out.println(list.get(i).toString());
}
    
2.2 Method bigSetClassifyString(String):

DESCRIPTION:
A static method that classifies (tags) every token of a string using the
fine tagset. All the tokens of the string must be separated by 
whitespace characters.

INPUT: String - the string containing the tokens.
OUTPUT: List <WordWithCategory> - a list of every token of the string 
with its guessed category (tag). 
		
EXAMPLE: 
List<WordWithCategory> list;
list = BigSetFunctions.bigSetClassifyString(" ÓôñáôéùôéêÝò 
   äõíÜìåéò ðéóôÝò óôïí óõíôáãìáôÜñ÷ç ÊáíôÜöé âïìâáñäßæïõí ôçí 
   ðüëç ÌéæïõñÜôá ôçò äõôéêÞò Ëéâýçò , ðïõ ôåëåß õðü ôïí Ýëåã÷ï 
   ôùí áíôéêáèåóôùôéêþí äõíÜìåùí , äÞëùóå êÜôïéêïò ôçò ðüëçò óôï 
   ðñáêôïñåßï Reuters . ");
for (int i=0;i<list.size();i++){
   System.out.println(list.get(i).toString());
}
			
EXAMPLE OUTPUT:
ÓôñáôéùôéêÝò adjective/nominative/feminine/plural/--
äõíÜìåéò noun/accusative/feminine/plural/--
ðéóôÝò adjective/accusative/feminine/plural/--
óôïí article/prepositional/accusative/masculine/singular
óõíôáãìáôÜñ÷ç noun/accusative/masculine/singular/--
ÊáíôÜöé noun/accusative/neuter/singular/--
âïìâáñäßæïõí verb/--/active/plural/present
ôçí article/definite/accusative/feminine/singular
ðüëç noun/accusative/feminine/singular/--
ÌéæïõñÜôá noun/accusative/feminine/singular/--
ôçò article/definite/genitive/feminine/singular
äõôéêÞò adjective/genitive/feminine/singular/--
Ëéâýçò noun/genitive/feminine/singular/--
, punctuation/--/--/--/--
ðïõ pronoun/inflectionless/--/--/--
ôåëåß verb/--/active/singular/present
õðü preposition/--/--/--/--
ôïí article/definite/accusative/masculine/singular
Ýëåã÷ï noun/accusative/masculine/singular/--
ôùí article/definite/genitive/neuter/plural
áíôéêáèåóôùôéêþí adjective/genitive/feminine/plural/--
äõíÜìåùí noun/genitive/feminine/plural/--
, punctuation/--/--/--/--
äÞëùóå verb/--/active/singular/past
êÜôïéêïò noun/nominative/masculine/singular/--
ôçò article/definite/genitive/feminine/singular
ðüëçò noun/genitive/feminine/singular/--
óôï article/prepositional/accusative/neuter/singular
ðñáêôïñåßï other/foreign_word/--/--/--
Reuters other/foreign_word/--/--/--
. punctuation/--/--/--/--
			
2.3 Method bigSetEvaluateFile(String):

DESCRIPTION:
A static method that computes the tagger's accuracy, given a file (in UTF-8 
encoding) containing a sequence of tokens and their correct fine categories 
(tags). The file must contain one line for each token, and each line must 
contain the token followed by the correct tag, separated by a space, as 
in the example output of the previous method. 

INPUT: String - the location of the file.
OUTPUT: double - the tagger's accuracy on the tokens of the input file. 

EXAMPLE:
System.out.println(BigSetFunctions.bigSetEvaluateFile("my_test_file.txt"));
			
2.4 Method bigSetTrainOtherClassifier(String):

DESCRIPTION:
A static method that trains the tagger on a file (in UTF-8 encoding) 
containing a sequence of tokens and their correct fine categories (tags). 
The file must be in the same format as the example output of method 2.2.

INPUT: String - the location of the file.
EXAMPLE:
BigSetFunctions.bigSetTrainOtherClassifier("my_train_fle.txt");

			
3. Public methods of class gr.aueb.cs.nlp.postagger.WordWithCategory:
---------------------------------------------------------------------

3.1 Method getCategory():

DESCRIPTION:
A static method that returns the category (tag) of a WordWithCategory pair.
			
OUTPUT: String - the category (tag) of the pair.  
		
EXAMPLE:
WordWithCategory wc = new WordWithCategory();
....
wc.getCategory();

3.2 Method getWord():

DESCRIPTION:
A static method that returns the word (token) of a WordWithCategory pair.
			
OUTPUT: String - the word (token) of the pair. 
		
EXAMPLE:
WordWithCategory wc = new WordWithCategory();
....
wc.getWord();
			
3.3 Method setWord(String):

DESCRIPTION:
A static method that sets the word (token) of a WordWithCategory pair.

INPUT: String - the word (token) to be stored in the pair.
		
EXAMPLE:
WordWithCategory wc = new WordWithCategory();
wc.setWord("êáôÜóôáóç");
		
3.4 Method setCategory(String):

DESCRIPTION:
A static method that sets the category (tag) of a WordWithCategory pair.

INPUT: String - the category (tag) to be stored in the pair. 
		
EXAMPLE:
WordWithCategory wc = new WordWithCategory();
wc.setCategory("verb/--/--/--/--");
	

Using the tagger from the command line:
=======================================

To run the tagger from the command line, go to the "bin" directory and 
use the following command:

> java -jar POStagger.jar OPTION FILE_TO_BE_TAGGED

Where OPTION is 0 (Coarse Tagset) or 1 (Fine Tagset) and FILE_TO_BE_TAGGED 
is the name of the file, which contains the text to be classified (in 
UTF-8 encoding).
		
Note: The system generates the file properties_test.txt, which is an 
intermediate output file, used for debugging purposes.

=== END OF FILE ===