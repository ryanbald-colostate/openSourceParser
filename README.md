# openSourceParser
Parser to identify libraries in source code. Research project with a huge pipeline that starts with this parser.
Works only with java, C# and C++.

It looks for and reads source code files (Java, C++ or C#) in a directory recursively. It updates the tables project, file, API and file_API. 

/*List of parameters:
		/*List of parameters:

		0: dirTrab ex: /Users/fabiomarcosdeabreusantos/Documents/dev/github/jabref/src

		1: format ex: java

		2: save in db ex: N

		3: save in csv ex: Y

		4: db name to save ex: dev

		5: db user ex: admin

		6: db password ex: 123

		7: project name ex: jabref

		8: outdir (csv) ex: /Users/fabiomarcosdeabreusantos/Documents/dev/github/jabref/

		9: list of reserved words to search (blank separated) ex:     import

		 */





Using the jar:


java -jar OSSParser.jar "/Volumes/GoogleDrive/My Drive/dev/javrefVersions/jabref-5.0-alpha" java N Y teste admin 123 jabref50 "/Users/fd252/OneDrive/Production/ETL1-Pipeline-main/data/outputs/new/jabref/" "import"
		

# Overview
openSourceParser is essentially the start of the data pipeline to create the binary outputs. There is not one linear path to the output but there are roughly 3 paths that go into OSSPRMapper4, which creates the outputs.

Here are the repos/files that make up the paths:

- openSourceParser -> [parseAPIPath](https://github.com/fabiojavamarcos/parseAPIPath) -> [labelAPILLM](https://github.com/ryanbald-colostate/labelAPILLM) -> API_specific.csv
- [ETL2-Pipeline](https://github.com/fabiojavamarcos/ETL2-Pipeline)(MergeDF -> updated_procIssues) -> [mapIssues2](https://github.com/fabiojavamarcos/mapIssues2) -> pr_issue table
- [ETL1-Pipeline](https://github.com/fabiojavamarcos/ETL1-Pipeline)(updated_Research2) -> filesPR3BodyTitle2.txt


Here are the the functions of [OSSPRMapper4](https://github.com/fabiojavamarcos/OSSPRMapper4):

- filesPR3BodyTitle2.txt, API_specific table, file table, and file_API table -> OSSPRMapper4(CSV=0) -> apriori and pr tables
- apriori, pr, and pr_issue tables -> OSSPRMapper4(CSV=1) -> binary outputs

Here is the diagram for the data pipeline:
<img width="3553" height="1753" alt="DataPipeline-v1 1 drawio" src="https://github.com/user-attachments/assets/67db0fd3-4480-4d22-ae51-2a57ec1ffad0" />
