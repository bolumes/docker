# Use a imagem oficial do PostgreSQL
FROM postgres:12

# Defina variáveis de ambiente (opcional, dependendo das necessidades do seu aplicativo)
ENV POSTGRES_DB=nome_do_banco_de_dados \
    POSTGRES_USER=seu_usuario \
    POSTGRES_PASSWORD=sua_senha

# Exponha a porta 5432 para conexões com o banco de dados
EXPOSE 5432

# Comando padrão para iniciar o servidor PostgreSQL quando o contêiner for iniciado
CMD ["postgres"]

