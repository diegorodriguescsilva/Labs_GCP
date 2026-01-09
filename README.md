# Labs_GCP

Etapa 1 – Preparação do ambiente
Nesta etapa, o ambiente Terraform é preparado. São criados os arquivos e diretórios do projeto, definidas as variáveis globais e configurado o provider do Google Cloud. Nenhum recurso é criado nesta fase; o objetivo é apenas organizar e inicializar o projeto para as próximas etapas do laboratório.

Etapa 2 (importação)
Etapa 3 (backend remoto)
Etapa 6 (VPC)
Etapa 7 (firewall)

# Ações da Etapa 1 :

1. Acessamos o Cloud Shell
Abrimos o Cloud Shell para ter um terminal já configurado com:
Terraform instalado
Acesso autenticado ao Google Cloud
Permissões no projeto do laboratório
Isso evita configurações manuais no computador local.

2. Criamos a estrutura do projeto Terraform
Criamos pastas e arquivos que organizam o código Terraform, separando responsabilidades:

Arquivos principais (main.tf, variables.tf)
Módulos para recursos específicos (instâncias e storage)
Essa organização facilita:
Leitura do código
Manutenção
Reutilização em outros projetos

3. Definimos variáveis globais

Criamos variáveis para:
Projeto do Google Cloud
Região
Zona
Essas variáveis permitem que o código:
Seja reutilizado em outros ambientes
Evite valores fixos espalhados nos arquivos
Fique mais seguro e flexível

4. Configuramos o Terraform e o provider Google Cloud

Configuramos:
Qual provider o Terraform deve usar (google)
Qual versão do provider é permitida
Em qual projeto, região e zona o Terraform vai operar
Isso permite que o Terraform saiba onde e como criar ou gerenciar recursos.

5. O que acontece ao executarmos a Etapa 1:


✔️ O projeto Terraform é criado e organizado
✔️ As variáveis do ambiente são definidas
✔️ O provider Google Cloud é configurado
✔️ O Terraform é inicializado (terraform init)

# Etapa 1 – Preparação do ambiente

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

Abra o arquivo ```variables.tf``` no Cloud Shell:

```nano variables.tf```

3.2 Cole o seguinte conteúdo dentro do arquivo, fazendo as alteraçoes necessárias:

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

3.3 - Salve e saia do editor:
Se estiver usando nano, pressione Ctrl+O → Enter → Ctrl+X.

# Passo 4 – Variáveis dos módulos
Você precisa criar os arquivos de variáveis dentro de cada módulo (instances e storage).

1️⃣ Módulo de instâncias ```(modules/instances/variables.tf)``

4.1 - Abra o arquivo:

```nano modules/instances/variables.tf```

4.2 - Cole o seguinte conteúdo dentro do arquivo, fazendo as alteraçoes necessárias:

```
variable "region" {
  description = "Região do recurso"
  type        = string
}



variable "zone" {
  description = "Zona do recurso"
  type        = string
}

variable "project_id" {
  description = "ID do projeto"
  type        = string
}
```

Salve (Ctrl+O → Enter) e saia (Ctrl+X).

2️⃣ Módulo de storage ```(modules/storage/variables.tf)```

1. Abra o arquivo:
```nano modules/storage/variables.tf```

2. E cole o mesmo conteúdo, já que são as mesmas variáveis:

```
variable "region" {
  description = "Região do recurso"
  type        = string
}

variable "zone" {
  description = "Zona do recurso"
  type        = string
}

variable "project_id" {
  description = "ID do projeto"
  type        = string
}
```
Salve e saia

# Passo 4 – Configurar Terraform e provedor no main.tf

1. Abra o main.tf:

```nano main.tf```

2. E cole o seguinte código:
```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 5.0"
    }
  }
}

provider "google" {
  project = var.project_id
  region  = var.region
  zone    = var.zone
}
```
# Próximo passo

Depois disso, você pode inicializar o Terraform:

```terraform init```
```terraform plan```
```terraform apply```
