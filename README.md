# Labs_GCP - Build Infrastructure with Terraform on Google Cloud

Neste repositório vamos aprender a criar, gerenciar e atualizar recursos na Google Cloud Platform (GCP) utilizando o Terraform, uma ferramenta de Infraestrutura como Código (IaC).

O que veremos:

- Estruturar projetos Terraform com módulos e variáveis;
- Criar e importar instâncias de máquinas virtuais no Compute Engine;
- Configurar backends remotos usando buckets do Cloud Storage;
- Atualizar e destruir recursos de forma segura;
- Criar redes VPC, sub-redes e regras de firewall;
- Utilizar módulos oficiais do Terraform Registry.

Com este repositório, qualquer pessoa poderá seguir o passo a passo e praticar gestão automatizada de infraestrutura na nuvem, adquirindo habilidades práticas em Terraform e GCP.


Etapa 1 – Preparação do ambiente
Nesta etapa, o ambiente Terraform é preparado. São criados os arquivos e diretórios do projeto, definidas as variáveis globais e configurado o provider do Google Cloud. Nenhum recurso é criado nesta fase; o objetivo é apenas organizar e inicializar o projeto para as próximas etapas do laboratório.

O que aprendemos:

- Acessar o Cloud Shell no Google Cloud
- Criar a estrutura de diretórios de um projeto Terraform
- Organizar o código usando módulos
- Definir variáveis (project, region, zone)
- Configurar o provider do Google Cloud
- Inicializar o Terraform

📌 Aprendizado principal:
Como preparar corretamente um projeto Terraform antes de criar qualquer recurso.

Etapa 2 – Importação da infraestrutura existente
Nesta etapa, recursos que já existiam no Google Cloud (máquinas virtuais) foram importados para o Terraform. Foram criadas configurações mínimas no código e utilizados comandos de importação para que o Terraform passasse a gerenciar essas instâncias. Nenhum recurso novo foi criado; o objetivo foi apenas assumir o controle da infraestrutura existente.

O que aprendemos:

- Identificar recursos já existentes no Google Cloud
- Escrever configurações mínimas para recursos existentes
- Importar instâncias já criadas para o Terraform
- Fazer o Terraform assumir o controle de recursos existentes
- Aplicar mudanças sem recriar recursos

📌 Aprendizado principal:
Como gerenciar recursos que não foram criados originalmente pelo Terraform.

Etapa 3 – Configuração de backend remoto
Nesta etapa, foi criado um bucket no Google Cloud Storage e configurado como backend remoto do Terraform. O estado da infraestrutura, que antes era local, foi migrado para esse bucket, permitindo maior segurança, persistência e colaboração. Essa etapa garante que o Terraform sempre saiba quais recursos estão sendo gerenciados.

O que aprendemos:

- Criar um bucket no Cloud Storage via Terraform
- Configurar um backend remoto para armazenar o estado
- Migrar o estado local para um backend remoto
- Entender a importância do arquivo de estado do Terraform

📌 Aprendizado principal:
Como armazenar o estado do Terraform de forma segura e compartilhável.

Etapa 4 – Modificação e atualização da infraestrutura
Nesta etapa, a infraestrutura foi modificada utilizando apenas código Terraform. Foram alterados os tipos de máquina de instâncias existentes e criada uma nova instância adicional. O Terraform comparou o estado atual com a configuração declarada e aplicou apenas as mudanças necessárias, demonstrando o controle e a escalabilidade da infraestrutura como código.

O que aprendemos:

- Alterar recursos existentes apenas modificando o código
- Atualizar tipos de máquina de instâncias
- Criar novas instâncias via Terraform
- Aplicar mudanças de forma incremental e controlada

📌 Aprendizado principal:
Como evoluir a infraestrutura de maneira segura usando Infraestrutura como Código.

Etapa 5 – Destruição controlada de recursos
Nesta etapa, um recurso foi removido da configuração Terraform, fazendo com que o Terraform destruísse automaticamente a infraestrutura correspondente. Essa abordagem garante que a exclusão de recursos seja feita de forma segura, controlada e consistente, sempre baseada no código.

O que aprendemos:

- Remover recursos apagando-os do código
- Destruir infraestrutura de forma segura com terraform apply
- Evitar exclusões manuais no Console
- Manter o estado do Terraform consistente

📌 Aprendizado principal:
Como remover recursos sem risco, usando apenas o código como fonte da verdade.

Etapa 6 – Criação de VPC e sub-redes com módulo do Registry
Nesta etapa, foi utilizado um módulo oficial do Terraform Registry para criar uma VPC personalizada e sub-redes no Google Cloud. As instâncias foram associadas às sub-redes corretas, garantindo organização, isolamento e gerenciamento de rede totalmente via código.

O que aprendemos:

- Utilizar módulos oficiais do Terraform Registry
- Criar uma VPC personalizada
- Criar e configurar sub-redes
- Conectar instâncias às sub-redes corretas
- Padronizar e reutilizar infraestrutura

📌 Aprendizado principal:
Como criar redes de forma profissional e reutilizável usando módulos prontos.

Etapa 7 – Configuração de regras de firewall
Nesta etapa, foi criada uma regra de firewall utilizando Terraform para permitir conexões de entrada na porta TCP 80 a partir de qualquer endereço IP. A regra foi associada à VPC criada anteriormente, demonstrando como políticas de segurança de rede podem ser definidas e gerenciadas como código.

O que aprendemos:

- Criar regras de firewall via Terraform
- Controlar tráfego de entrada na rede
- Permitir conexões TCP na porta 80
- Gerenciar segurança como código

📌 Aprendizado principal:
Como aplicar políticas de segurança de rede de forma automatizada e versionada.

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


# Etapa 5 – Destruição controlada de recursos

Serve para remover recursos da infraestrutura de forma controlada, usando apenas o código Terraform.
Em vez de apagar recursos manualmente no Console do Google Cloud, o Terraform faz isso de forma:

- Segura
- Rastreável
- Controlada
- Baseada em código

# O que vamos fazer na etapa 5:

1️⃣ Removemos o recurso do código Terraform

Apagamos do arquivo de configuração o recurso da instância:

```tf-instance-748118```
Isso indica ao Terraform que essa instância não deve mais existir.

Inicializamos novamente o Terraform

Executamos:
```terraform init```

3️⃣ Aplicamos as mudanças

```terraform apply```

# O que acontece ao executarmos a Etapa 5:


✔️ Um recurso é destruído automaticamente
✔️ A remoção segue exatamente o que está no código
✔️ O estado do Terraform é atualizado
✔️ Não há risco de apagar recursos errados manualmente

# Passo 1: Abrir o arquivo do módulo instances

```nano modules/instances/instances.tf```

# Passo 2: Remover o recurso da terceira instância

Localize este bloco (instância 3) e apague todo ele:

```
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

Fique com apenas as instâncias 1 e 2 no arquivo.

Salve e saia do nano (Ctrl+O, Enter, Ctrl+X).

# Passo 3: Inicializar e aplicar

```terraform init```
```terraform apply```

Resultado esperado:

- tf-instance-1 e tf-instance-2 continuam existindo.
- tf-instance-748118 é destruída no GCP.

# Etapa 6 – Criação de VPC e sub-redes com módulo do Registry

Etapa 6 serve para criar e gerenciar a rede da infraestrutura (VPC e sub-redes) usando um módulo oficial do Terraform Registry.

Essa etapa mostra como:

- Evitar criar tudo do zero
- Usar módulos prontos e confiáveis
- Padronizar a criação de redes

# O que vamos fazer na etapa 6:
1️⃣ Utilizamos um módulo oficial do Terraform Registry

Adicionamos ao main.tf o módulo Network do Terraform Registry, usando:

- Versão específica (10.0.0)
- Configuração compatível com o laboratório
- Isso garante estabilidade e boas práticas.

2️⃣ Criamos uma VPC personalizada com sub-redes

Usando o módulo, criamos:

- Uma VPC chamada tf-vpc-781719
- Modo de roteamento global

Duas sub-redes na região us-east1:

- subnet-01 → 10.10.10.0/24
- subnet-02 → 10.10.20.0/24

Nenhuma rota ou IP secundário foi configurado, pois não era necessário.

3️⃣ Conectamos as instâncias às sub-redes corretas

Atualizamos o arquivo instances.tf para:

- Conectar tf-instance-1 à subnet-01
- Conectar tf-instance-2 à subnet-02
- Associar as instâncias à VPC criada

Isso garante organização e isolamento de rede.

# O que acontece ao executarmos a Etapa 6:


✔️ Uma nova VPC é criada
✔️ Sub-redes personalizadas são provisionadas
✔️ Instâncias são conectadas às sub-redes corretas
✔️ A rede passa a ser gerenciada via código

# Passo 1: Adicionar o módulo Network ao ```main.tf```

Abra o arquivo:
```nano main.tf```

Adicione logo abaixo dos outros módulos:

```
# Módulo do Terraform Registry: Network
module "vpc_network" {
  source  = "terraform-google-modules/network/google"
  version = "10.0.0"

  project_id   = var.project_id
  network_name = "tf-vpc-781719"
  routing_mode = "GLOBAL"

  subnets = [
    {
      subnet_name   = "subnet-01"
      subnet_ip     = "10.10.10.0/24"
      subnet_region = "us-east1"
    },
    {
      subnet_name   = "subnet-02"
      subnet_ip     = "10.10.20.0/24"
      subnet_region = "us-east1"
    }
  ]
}
```

Explicação:

- network_name → nome da VPC
- routing_mode → GLOBAL, conforme o lab
- subnets → define 2 sub-redes com nomes, IPs e região

Salve e saia do nano (Ctrl+O, Enter, Ctrl+X).

# Passo 2: Inicializar o Terraform para baixar o módulo

```terraform init```

O Terraform vai baixar a versão 10.0.0 do módulo terraform-google-modules/network/google.

# Passo 3: Aplicar a criação da rede e sub-redes

```terraform apply```

Isso vai criar a VPC tf-vpc-781719 e as sub-redes subnet-01 e subnet-02 no GCP.

# Passo 4: Conectar as instâncias às sub-redes
Agora abra o arquivo do módulo instances:

```nano modules/instances/instances.tf```

Atualize cada instância para usar a nova VPC e sub-rede.

```

# Instância 1 conectada à subnet-01
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
    network    = "tf-vpc-781719"
    subnetwork = "subnet-01"
    access_config {}
  }

  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  allow_stopping_for_update = true
}

# Instância 2 conectada à subnet-02
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
    network    = "tf-vpc-781719"
    subnetwork = "subnet-02"
    access_config {}
  }

  metadata_startup_script = <<-EOT
        #!/bin/bash
  EOT

  allow_stopping_for_update = true
}

```

Certifique-se de manter o bloco access_config {} para que cada VM tenha IP externo (se necessário).

Salve e saia do nano.

# Passo 5: Aplicar as mudanças nas instâncias

```terraform apply```

Isso vai mover as instâncias para as sub-redes corretas na nova VPC.

Resultado esperado:

- VPC tf-vpc-781719 criada.
- Sub-redes subnet-01 e subnet-02 criadas na região us-east1.
- tf-instance-1 conectada à subnet-01.
- tf-instance-2 conectada à subnet-02.

# Etapa 7: Configurar uma regra de firewall

Serve para controlar o tráfego de rede usando regras de firewall, garantindo que apenas conexões permitidas possam acessar os recursos. Essa etapa mostra como segurança também é gerenciada como código, usando Terraform.

# O que vamos fazer na etapa 7:

1️⃣ Criamos uma regra de firewall via Terraform

Criamos um recurso google_compute_firewall chamado tf-firewall.

Essa regra:
- Está associada à VPC tf-vpc-781719
- Permite conexões de entrada (ingress)
- Autoriza tráfego TCP na porta 80
- Aceita conexões de qualquer IP (0.0.0.0/0)

2️⃣ Associamos a regra à rede correta

Indicamos explicitamente a rede da VPC usando o self_link ou ID da rede.
Isso garante que a regra:

- Afete apenas a VPC criada no laboratório
- Não impacte outras redes do projeto

3️⃣ Aplicamos as mudanças
```terraform init```
```terraform apply```

# O que acontece ao executarmos a Etapa 7:

✔️ Uma regra de firewall é criada
✔️ A VPC passa a aceitar tráfego HTTP (porta 80)
✔️ A segurança da rede é gerenciada via código
✔️ As regras ficam versionadas e documentadas


Passo 1: Editar o ```main.tf```

```nano main.tf```

Role até o final do arquivo e adicione este recurso (faça as alterações de network que precisa):

```

resource "google_compute_firewall" "tf_firewall" {
  name    = "tf-firewall"
  network = "projects/${var.project_id}/global/networks/tf-vpc-781719"

  allow {
    protocol = "tcp"
    ports    = ["80"]
  }

  source_ranges = ["0.0.0.0/0"]
}

```

# Passo 2: Inicializar o Terraform

Sempre que adicionamos um novo recurso:

```terraform init```

# Passo 3: Passo 3: Aplicar as mudanças

```terraform apply```

O Terraform irá:

- Criar a regra de firewall tf-firewall
- Permitir acesso TCP na porta 80 para toda a internet

Resultado esperado:

Após o apply, você terá:

- Regra de firewall tf-firewall
- Associada à VPC tf-vpc-781719
- Porta TCP 80 liberada para 0.0.0.0/0