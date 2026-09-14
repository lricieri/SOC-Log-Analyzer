# SOC Log Analyzer

Ferramenta de triagem de nível 1 para logs de autenticação, simulando as
primeiras verificações feitas por um analista em um SOC (Security
Operations Center) ao investigar alertas de acesso suspeito.

## O que ela detecta

| Padrão | Severidade | Descrição |
|---|---|---|
| Força bruta | Alta | Muitas tentativas de login falhas vindas do mesmo IP |
| Password spraying | Alta | O mesmo IP tentando login contra vários usuários diferentes |
| Login fora do horário | Média | Login bem-sucedido fora do horário comercial (22h–6h) |
| Sucesso após falhas | Crítica | Login bem-sucedido logo depois de uma sequência de falhas - possível indício de credencial comprometida |

## Como rodar

```bash
python analyzer.py logs/auth_sample.csv
```

O arquivo de log de entrada é um CSV simples, no formato:

```csv
timestamp,ip,usuario,status
2026-09-09 14:02:10,203.0.113.55,admin,fail
```

## Exemplo de saída

```
Eventos analisados: 19
Alertas gerados: 6

[CRITICA] sucesso_apos_falhas — IP 192.0.2.77
    login de 'carlos.pereira' teve sucesso apos 3 falhas seguidas

[ALTA] forca_bruta — IP 203.0.113.55
    6 tentativas de login falhas
```

## Motivação

Este projeto simula a primeira etapa do trabalho de um analista de SOC:
transformar um log bruto em uma lista de alertas priorizados por
severidade, prontos para triagem e escalonamento. o repositório visa focar em monitoramento de segurança (SIEM, triagem de alertas,
resposta inicial a incidentes).

## Próximos passos

- [ ] Ler logs diretamente no formato syslog/auth.log real
- [ ] Adicionar geolocalização de IP para detectar "impossible travel"
- [ ] Exportar alertas em JSON para integração com outras ferramentas

## Tecnologias

- Python 3 (biblioteca padrão apenas - sem dependências externas)
"# SOC-Log-Analyzer" 
