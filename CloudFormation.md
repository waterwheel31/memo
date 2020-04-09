# Memo for Cloud Formation (using AWS)

- Create stack 

```
aws cloudformation create-stack
--stack-name <myfirsttest>
--region <us-west-2>
--template-body file://<testconfig.yml> 
```



- Update stack 

```
aws cloudformation update-stack
--stack-name <myfirsttest>
--region <us-west-2>
--template-body file://<testconfig.yml> 
```




- Charting softwares
    - Lucidchart https://www.lucidchart.com/