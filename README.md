# projeto-dio

Um ecossistema que pega um arquivo que está no bucket da s3, conta as palavras do arquivo, e envia de volta pra s3. Cria uma maquina EMR pelo arquivo mrjob, e sobe essa contagem de palavras através de um script python.

1 - 
Criar um bucket na s3, e criar 3 pastas com os seguintes nomes:
data
output
temp

2 - 
Acessar o EC2 e em painel clicar em Pares de chaves, para criar um arquivo .pem

3 - 
Do lado da região, no canto superior direito clicar em: <conta> - minhas credenciais de segurança

criar chaves de acesso e fazer o download do arquivo com as achaves
  
4 -
 Dentro do linux, criar um ambiente virtual python

Criar ambiente virtual python: virtualenv --python=python3.8 venv_diolive
Ativa o ambiente virtual python: source venv_teste/bin/activate
OBS: tem que colocar o endereço de onde está a maquina virtual, achar o arquivo activate, só assim o comando acima vai funcionar, como foi feito

- 5
 Precisa instalar as duas bibliotecas abaixo 
Instalar boto3: pip install boto3
Instalar mrjob: pip install mrjob
  
6 -
Configurar o arquivo mrjob.conf
aws_access_key_id e aws_secret_access_key são as informações que estão na chave que foi criada em minhas credenciais
ec2_key_pair: <nome_arquivo> nome exato do arquivo que foi baixado com a extensão .pem
ec2_key_pair_file: <endereço do arquivo .pem>
region: <regiao>
ssh_tunnel: true //deixar como true
instance_type: m5.xlarge  //pode manter essa maquina
num_core_instances: 3 //define o numero de instancias, pode deixar tbm
  
7 - 
realizar o comando abaixo dentro do diretorio que esta o arquivo dio-live-wordcount-test-py:
python3 dio-live-wordcount-test.py -r emr s3://{your_s3_bucket_name}/data/SherlockHolmes.txt --output-dir=s3://{your_s3_bucket_name}/output/logs1 --cloud-tmp-dir=s3://{your_s3_bucket_name}/temp/
  
