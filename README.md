# Grafana

- Grafana Loki - Dashboard, gerenciamento e organização dos dados
- Fluent bit - Coletor via udp e Ingestor de dados no loki.

Sugestão de implementação
```
const dgram = require('dgram');
const client = dgram.createSocket('udp4');

function log(app, message, level) {
    const logMessage = {
        app: app,
        timestamp: new Date().toISOString(),
        level: level,
        message: message
    };
    const messageBuffer = Buffer.from(JSON.stringify(logMessage));

    client.send(messageBuffer, 0, messageBuffer.length, 24224, ID_SERVER_LOKI, (err) => {
        if (err) {
            console.error('Erro ao enviar mensagem', err);
        }
    });
}

log('meu_app', 'Msg de erro', error);

```
