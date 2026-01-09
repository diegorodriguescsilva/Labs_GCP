# Labs_GCP

# Passo 1: Abrir o Cloud Shell
No console do Google Cloud, clique no ícone do Cloud Shell (canto superior direito).
Aguarde até abrir o terminal.

# Passo 2: Criar a estrutura de diretórios

No terminal do Cloud Shell, execute os seguintes comandos:

# Criar diretório principal do projeto (opcional)
```
mkdir terraform-lab
cd terraform-lab
```

# Criar arquivos principais
```
touch main.tf 
variables.tf
```
# Criar diretórios de módulos
```
mkdir -p modules/instances
mkdir -p modules/storage
```
# Criar arquivos de módulos
```
touch modules/instances/instances.tf modules/instances/outputs.tf modules/instances/variables.tf
touch modules/storage/storage.tf modules/storage/outputs.tf modules/storage/variables.tf
```
# Estrutura do repositório:
terraform-lab/
│
├── main.tf
├── variables.tf
└── modules/
    ├── instances/
    │   ├── instances.tf
    │   ├── outputs.tf
    │   └── variables.tf
    └── storage/
        ├── storage.tf
        ├── outputs.tf
        └── variables.tf

# Passo 3: Definir variáveis

3.1 Variáveis do diretório raiz (variables.tf)

Abra o arquivo ```variables.tf`` no Cloud Shell:

```
nano variables.tf
````
3.2 Cole o seguinte conteúdo dentro do arquivo, fazendo as alteraçÕes necessárias:

```
# Variável que define a região do Google Cloud onde os recursos serão criados
# No laboratório, esse valor é preenchido automaticamente no início
variable "region" {
  description = "Região do Google Cloud"
  default     = "<filled in at lab start>"
}

# Variável que define a zona específica dentro da região
# Zonas são usadas principalmente para recursos como máquinas virtuais
variable "zone" {
  description = "Zona do Google Cloud"
  default     = "<filled in at lab start>"
}

# Variável que define o ID do projeto do Google Cloud
# Esse ID identifica de forma única o projeto onde o Terraform irá gerenciar os recursos
variable "project_id" {
  description = "ID do projeto do Google Cloud"
  default     = "qwiklabs-gcp-00-b38f2f11b459"
}

```