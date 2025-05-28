# PHPIPAM com Docker Compose

Este repositório contém a configuração do [PHPIPAM](https://phpipam.net/) utilizando Docker Compose. Ele permite implantar facilmente o PHPIPAM com um banco de dados MariaDB.

## Pré-requisitos

*   [Docker](https://docs.docker.com/get-docker/)
*   [Docker Compose](https://docs.docker.com/compose/install/) (geralmente incluído com o Docker Desktop ou instalado como plugin do Docker CLI)

## Configuração

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/Lauri-Zancanaro/phpIPAM-docker.git
    cd phpIPAM-docker
    ```

2.  **Crie o arquivo de ambiente:**
    Copie o arquivo de exemplo `.env.example` para `.env`:
    ```bash
    cp .env.example .env
    ```

3.  **Edite o arquivo `.env`:**
    Abra o arquivo `.env` em um editor de texto e defina senhas seguras para `MYSQL_ROOT_PASSWORD` e `IPAM_DB_PASSWORD`. Você também pode ajustar `TZ` (fuso horário) e `SCAN_INTERVAL` se necessário.
    ```dotenv
    # Arquivo .env
    MYSQL_ROOT_PASSWORD=sua_senha_root_muito_segura
    IPAM_DB_PASSWORD=outra_senha_phpipam_segura
    # TZ=America/Sao_Paulo # Exemplo
    # SCAN_INTERVAL=2h # Exemplo
    ```
    **Importante:** Nunca comite o arquivo `.env` com suas senhas para o repositório Git.

## Execução

1.  **Inicie os contêineres:**
    No diretório do projeto, execute:
    ```bash
    docker compose up -d
    ```
    Isso baixará as imagens (se ainda não existirem) e iniciará os serviços em segundo plano (`-d`).

2.  **Acesse o PHPIPAM:**
    Abra seu navegador e acesse `http://localhost` (ou o IP do seu servidor Docker se não estiver rodando localmente). A configuração inicial do PHPIPAM será apresentada na primeira vez.

## Serviços

*   **`phpipam-web`:** O serviço web principal do PHPIPAM, acessível na porta 80.
*   **`phpipam-cron`:** Executa tarefas agendadas do PHPIPAM (ex: verificação de status de hosts).
*   **`phpipam-mariadb`:** O banco de dados MariaDB para armazenar os dados do PHPIPAM.

## Volumes

*   **`phpipam-db-data`:** Persiste os dados do banco de dados MariaDB.
*   **`phpipam-logo`:** Permite substituir o logo padrão do PHPIPAM (opcional, monte seu arquivo de logo neste volume se desejar).
*   **`phpipam-ca`:** Permite adicionar certificados CA confiáveis (opcional).

## Parando os Serviços

Para parar os contêineres:
```bash
docker compose down
```
Isso para e remove os contêineres, mas os volumes (como `phpipam-db-data`) são preservados.

## Contribuição

Sinta-se à vontade para abrir issues ou pull requests se encontrar problemas ou tiver sugestões de melhoria.

