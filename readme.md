# SA-SQL
The code for the paper SA-SQL: A Schema-Aligned Collaborative Framework for Text-to-SQL ([https://openreview.net/forum?id=YBlNfpbjIrp](https://openreview.net/forum?id=YBlNfpbjIrp))

## Prepare Spider Data

Download [spider data](https://drive.google.com/uc?export=download&id=1TqleXec_OykOYFREKKtschzY29dUcVAQ) and database (only spider original database right now) and then unzip them:

```shell
mkdir data 
unzip spider.zip 
mv spider/database . 
mv spider data
```

### Run Inference 
Run the command below, and the predicted sql will be save to the file named "predicted_sql.txt"
```shell
bash run_SASQL.sh 
```

## Run evaluation 
Add your openai key in the *generate.py*  files. 
```shell
openai.api_key = "your_api_key"
```

Clone evaluation scripts (test-suite-sql-eval:[https://github.com/taoyds/test-suite-sql-eval](https://github.com/taoyds/test-suite-sql-eval)): 

```shell
mkdir third_party
cd third_party
git clone https://github.com/taoyds/test-suite-sql-eval
cd ..
```


Put the 'predicted_sql.txt' in the current directory. 

Then you can run evaluation with following command, and you will see the results on dev data.  
For testing, you just need to replace '**dev_gold.sql**' with your test data, folder '**database**' with your database and '**spider/tables.json**' with your test tables.json. 
```shell
python third_party/test-suite-sql-eval/evaluation.py --gold dev_gold.sql --pred predicted_sql.txt --db database --table data/spider/tables.json --etype all 
```
