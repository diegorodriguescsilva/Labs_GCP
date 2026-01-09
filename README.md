# Labs_GCP

Etapa 1 – Preparação do ambiente
Nesta etapa, o ambiente Terraform é preparado. São criados os arquivos e diretórios do projeto, definidas as variáveis globais e configurado o provider do Google Cloud. Nenhum recurso é criado nesta fase; o objetivo é apenas organizar e inicializar o projeto para as próximas etapas do laboratório.

Etapa 2 – Importação da infraestrutura existente
Nesta etapa, recursos que já existiam no Google Cloud (máquinas virtuais) foram importados para o Terraform. Foram criadas configurações mínimas no código e utilizados comandos de importação para que o Terraform passasse a gerenciar essas instâncias. Nenhum recurso novo foi criado; o objetivo foi apenas assumir o controle da infraestrutura existente.

Etapa 3 – Configuração de backend remoto
Nesta etapa, foi criado um bucket no Google Cloud Storage e configurado como backend remoto do Terraform. O estado da infraestrutura, que antes era local, foi migrado para esse bucket, permitindo maior segurança, persistência e colaboração. Essa etapa garante que o Terraform sempre saiba quais recursos estão sendo gerenciados.

Etapa 4 – Modificação e atualização da infraestrutura
Nesta etapa, a infraestrutura foi modificada utilizando apenas código Terraform. Foram alterados os tipos de máquina de instâncias existentes e criada uma nova instância adicional. O Terraform comparou o estado atual com a configuração declarada e aplicou apenas as mudanças necessárias, demonstrando o controle e a escalabilidade da infraestrutura como código.

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

# Etapa 2  - Importando uma VM para dentro do Terraform:

Nesta etapa, importamos recursos existentes dentro do GCP para dentro do terraform. 

1️⃣ Identificamos as instâncias já existentes
No Console do Google Cloud, verificamos que já existiam duas VMs criadas previamente pelo laboratório:

```tf-instance-1```
```tf-instance-2```

Também conferimos informações importantes como:
- Zona
- Tipo de máquina
- Imagem do sistema operacional
- Rede utilizada

Esses dados são necessários para escrever corretamente o código Terraform.

2️⃣ Criamos a configuração mínima das instâncias

Criamos os recursos ```google_compute_instance``` no módulo instances, mas com uma configuração mínima, apenas com os campos exigidos pelo laboratório, como:

- machine_type
- boot_disk
- network_interface
- metadata_startup_script
- allow_stopping_for_update

Essa configuração não cria novas VMs, ela apenas descreve como as VMs existentes são.

3️⃣ Importamos as instâncias para o estado do Terraform

Usamos o comando terraform import para associar:

- O recurso real do Google Cloud com o recurso descrito no código Terraform
exemplo:
```terraform import module.instances.google_compute_instance.tf-instance-1 tf-instance-1```
Após isso, o Terraform passou a controlar essas instâncias.

4️⃣ Aplicamos as mudanças

Executamos ```terraform apply```.

Como a configuração não estava completa, o Terraform fez ajustes leves nas instâncias existentes, o que foi permitido pelo laboratório.
Nenhuma instância foi recriada.

# O que acontece ao executarmos a Etapa 2:
✔️ O Terraform passa a gerenciar instâncias que já existiam
✔️ O estado do Terraform é atualizado com recursos reais
✔️ As VMs ficam sob controle do código
✔️ Mudanças futuras podem ser feitas via Terraform

# Passo 1: Observar as instâncias existentes: (Observe o cenário atual para que o Lab funcione corretamente)

No Console do Google Cloud:
Menu de navegação → Compute Engine → Instâncias de VM.

Verifique as instâncias criadas: ```tf-instance-1``` e ```tf-instance-2```.

Anote os seguintes dados:

- ID da instância (geralmente é o nome mesmo)
- Tipo de máquina (machine_type, normalmente e2-medium no lab)
- Imagem do disco de inicialização (debian-11 ou debian-10)
- Zona (usada nas variáveis)

Esses dados serão usados para escrever a configuração mínima no Terraform.

# Passo 2: Adicionar referência do módulo no main.tf

Abra o arquivo:

```nano main.tf```

Adicione abaixo do bloco do provider:

```
module "instances" {
  source     = "./modules/instances"
  project_id = var.project_id
  region     = var.region
  zone       = var.zone
}

```
Salve (Ctrl+O, Enter) e saia (Ctrl+X).

Reinicialize o Terraform:
```terraform init```

# Passo 3: Criar a configuração mínima no módulo ```instances``` 

1. Abra o arquivo do módulo:

```nano modules/instances/instances.tf```

2. Configurando o módulo ```instances.tf``` com o tipo de máquina correto

```
# Define a primeira instância de máquina virtual no Google Compute Engine
resource "google_compute_instance" "tf-instance-1" {

  # Nome da instância no Google Cloud
  name = "tf-instance-1"

  # Tipo de máquina (define CPU e memória)
  # e2-micro é um tipo leve e econômico, comum em laboratórios
  machine_type = "e2-micro"

  # Zona onde a instância será criada
  # O valor é obtido a partir da variável definida no projeto
  zone = var.zone

  # Configuração do disco de inicialização da VM
  boot_disk {
    initialize_params {
      # Imagem do sistema operacional usada na instância
      image = "debian-cloud/debian-11"
    }
  }

  # Configuração da interface de rede da instância
  network_interface {
    # Conecta a VM à rede VPC padrão do projeto
    network = "default"

    # Habilita um IP externo para permitir acesso à internet
    access_config {}
  }

  # Script executado automaticamente quando a instância inicia
  # Neste laboratório o script está vazio, apenas com o shebang
  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  # Permite que o Terraform pare e reinicie a instância
  # quando for necessário aplicar atualizações
  allow_stopping_for_update = true
}

# Define a segunda instância de máquina virtual no Google Compute Engine
resource "google_compute_instance" "tf-instance-2" {

  # Nome da segunda instância no Google Cloud
  name = "tf-instance-2"

  # Tipo de máquina utilizado (CPU e memória)
  machine_type = "e2-micro"

  # Zona onde a instância será criada
  zone = var.zone

  # Disco de inicialização da segunda instância
  boot_disk {
    initialize_params {
      # Sistema operacional da VM
      image = "debian-cloud/debian-11"
    }
  }

  # Interface de rede da segunda instância
  network_interface {
    # Utiliza a rede VPC padrão
    network = "default"

    # Habilita IP externo
    access_config {}
  }

  # Script de inicialização da instância
  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  # Permite interrupção da instância para atualizações via Terraform
  allow_stopping_for_update = true
}

```

# Passo 3: Reinicializar o Terraform
```terraform init```

# Passo 4: Importar as instâncias
```terraform import module.instances.google_compute_instance.tf-instance-1 tf-instance-1```
```terraform import module.instances.google_compute_instance.tf-instance-2 tf-instance-2```

# Etapa 3 - Configure um back-end remoto

Na etapa 3, configuramos para armazenar o estado do Terraform em um local remoto e seguro, em vez de deixar esse estado apenas no computador/local do Cloud Shell.
O estado do Terraform é um arquivo que guarda:

- Quais recursos existem
- Como eles estão configurados
- O que o Terraform gerencia no projeto

Sem esse arquivo, o Terraform não sabe o que já foi criado ou importado.

# O que vamos fazer na etapa 3:

1️⃣ Criamos um bucket no Cloud Storage

Criamos um bucket no Google Cloud Storage usando o Terraform, com as seguintes características:

- Nome único do bucket
- Localização nos EUA
- Exclusão forçada habilitada
- Controle de acesso uniforme

Esse bucket será usado exclusivamente para armazenar o estado do Terraform.

2️⃣ Adicionamos o bucket como backend remoto

Configuramos o Terraform para usar esse bucket como backend remoto.

Isso significa que:

- O arquivo ```terraform.tfstate``` deixa de ficar local
- O estado passa a ser salvo no Cloud Storage
- O estado pode ser compartilhado entre equipes
- O risco de perda do estado é reduzido

Também definimos um prefixo (terraform/state) para organizar o estado dentro do bucket.

3️⃣ Migramos o estado local para o backend remoto

Ao executar terraform init após configurar o backend, o Terraform perguntou se deveria:

- copiar o estado local para o novo backend remoto

Respondemos yes, e o estado foi migrado com sucesso.

# O que acontece ao executarmos a Etapa 3:

✔️ Um bucket de armazenamento é criado (se ainda não existir)
✔️ O Terraform passa a usar um backend remoto
✔️ O estado local é migrado para o Cloud Storage
✔️ O estado fica centralizado, seguro e persistente

# Passo 1: Criar módulo storage

No diretório do módulo storage, abra ou crie o arquivo ```storage.tf:```

```nano modules/storage/storage.tf```

E adicione a configuração do bucket:
```
resource "google_storage_bucket" "tf_bucket" {
  name                        = "tf-bucket-876542"
  location                    = "US"
  force_destroy               = true
  uniform_bucket_level_access = true
}
```

# Passo 2: Adicionar referência do módulo storage no main.tf

Abra ```main.tf:```

```nano main.tf```

E adicione abaixo do módulo instances:

```
module "storage" {
  source = "./modules/storage"
}
```

Salve e saia.

# Passo 3: Inicializar e aplicar para criar o bucket

No terminal:

```terraform init```
```terraform apply```

# Passo 4: Configurar o bucket como back-end remoto

No ```main.tf```, adicione no topo do arquivo (antes do bloco terraform { required_providers ... }) ou crie um arquivo separado chamado backend.tf:

```
terraform {
  backend "gcs" {
    bucket = "tf-bucket-876542"
    prefix = "terraform/state"
  }
}
```

# Passo 5: Inicializar o Terraform com o back-end remoto
No terminal:

```terraform init```

# Etapa 4 - Modificação e atualização da infraestrutura

Etapa 4 serve para modificar e evoluir a infraestrutura usando código, mostrando o principal poder do Terraform:
alterar recursos existentes de forma controlada e automática.

# O que vamos fazer na etapa 4:


1️⃣ Alteramos o tipo de máquina de instâncias existentes

Modificamos o código Terraform para:

- Atualizar tf-instance-1 para um tipo de máquina maior
- Atualizar tf-instance-2 para um tipo de máquina diferente

Terraform identificou essas mudanças e aplicou as alterações sem recriar as instâncias.

2️⃣ Criamos uma nova instância via código

Adicionamos no módulo instances um novo recurso:

```tf-instance-748118```

Essa instância não existia antes e foi criada exclusivamente via Terraform, seguindo o mesmo padrão das outras.

3️⃣ Aplicamos as mudanças com Terraform

Executamos:
```terraform init```
```terraform apply```

O Terraform:

- Comparou o estado atual com o código
- Mostrou um plano de mudanças
- Aplicou apenas o que foi necessário

# O que acontece ao executarmos a Etapa 4:

✔️ Tipos de máquina das VMs existentes são atualizados
✔️ Uma nova VM é criada automaticamente
✔️ As mudanças são feitas de forma segura e previsível
✔️ Tudo fica registrado no estado do Terraform

# Passo 1: Abrir o arquivo do módulo instances

```nano modules/instances/instances.tf```

# Passo 2: Alterar os tipos de máquina das instâncias existentes
Substitua:

```machine_type = "e2-micro"```

Por:

```
resource "google_compute_instance" "tf-instance-1" {
  name         = "tf-instance-1"
  machine_type = "e2-standard-2"  # Alterado
  ...
}

resource "google_compute_instance" "tf-instance-2" {
  name         = "tf-instance-2"
  machine_type = "e1-standard-2"  # Alterado
  ...
}
```

# Passo 3: Adicionar uma nova instância

```
# Instância 1
resource "google_compute_instance" "tf-instance-1" {
  name         = "tf-instance-1"
  machine_type = "e2-standard-2"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }

  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  allow_stopping_for_update = true
}

# Instância 2
resource "google_compute_instance" "tf-instance-2" {
  name         = "tf-instance-2"
  machine_type = "e2-standard-2"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }

  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  allow_stopping_for_update = true
}

# Instância 3 (nova)
resource "google_compute_instance" "tf-instance-748118" {
  name         = "tf-instance-748118"
  machine_type = "e2-standard-2"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }

  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  allow_stopping_for_update = true
}
```

Salve o arquivo.

Rode:

```terraform init```
```terraform apply```


# Etapa 5: 

Passo 1: Abrir o arquivo do módulo instances