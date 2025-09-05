# Instruções para Configuração do reCAPTCHA - Task AI

## 🔒 Implementação do reCAPTCHA

O formulário de contato da Task AI foi configurado com o Google reCAPTCHA v2 para proteção contra spam e bots.

## ⚙️ Configuração Atual

### Chave de Teste (Desenvolvimento)
- **Site Key**: `6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI`
- **Secret Key**: `6LeIxAcTAAAAAGG-vFI1TnRWxMZNFuojJ4WifJWe`
- **Status**: Chave de teste do Google (funciona apenas em localhost)

## 🚀 Configuração para Produção

### 1. Criar Conta no Google reCAPTCHA
1. Acesse: https://www.google.com/recaptcha/admin
2. Faça login com sua conta Google
3. Clique em "Criar" para adicionar um novo site

### 2. Configurar o Site
- **Rótulo**: Task AI - Formulário de Contato
- **Tipo de reCAPTCHA**: reCAPTCHA v2 ("Não sou um robô")
- **Domínios**: 
  - `taskai.com`
  - `www.taskai.com`
  - `localhost` (para desenvolvimento)

### 3. Obter as Chaves
Após a configuração, você receberá:
- **Site Key**: Chave pública (usada no HTML)
- **Secret Key**: Chave privada (usada no backend)

### 4. Atualizar o Código
Substitua a chave de teste no arquivo `contato.html`:

```html
<!-- Substituir esta linha -->
<div class="g-recaptcha" data-sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"></div>

<!-- Por esta (com sua chave real) -->
<div class="g-recaptcha" data-sitekey="SUA_CHAVE_SITE_AQUI"></div>
```

## 🔧 Funcionalidades Implementadas

### Validação Frontend
- ✅ Verificação se o reCAPTCHA foi preenchido
- ✅ Validação de todos os campos obrigatórios
- ✅ Verificação do checkbox de privacidade
- ✅ Feedback visual para campos com erro
- ✅ Reset do formulário após envio

### Validação Backend (Recomendada)
Para produção, implemente também a validação no servidor:

```javascript
// Exemplo em Node.js
const axios = require('axios');

async function verifyRecaptcha(token, secretKey) {
    const response = await axios.post('https://www.google.com/recaptcha/api/siteverify', {
        secret: secretKey,
        response: token
    });
    
    return response.data.success;
}
```

## 📋 Checklist de Implementação

### Desenvolvimento
- [x] Script do reCAPTCHA adicionado
- [x] Widget do reCAPTCHA implementado
- [x] Validação JavaScript configurada
- [x] Estilização com Tailwind CSS

### Produção
- [ ] Criar conta no Google reCAPTCHA
- [ ] Configurar domínios do site
- [ ] Obter chaves de produção
- [ ] Atualizar chave no código
- [ ] Implementar validação no backend
- [ ] Testar em ambiente de produção

## 🎨 Personalização Visual

### Estilo Atual
- **Posicionamento**: Centralizado no formulário
- **Tema**: Automático (se adapta ao tema do site)
- **Tamanho**: Padrão do Google

### Opções de Personalização
```html
<!-- Tema escuro -->
<div class="g-recaptcha" data-sitekey="SUA_CHAVE" data-theme="dark"></div>

<!-- Tamanho compacto -->
<div class="g-recaptcha" data-sitekey="SUA_CHAVE" data-size="compact"></div>

<!-- Tamanho invisível (v3) -->
<div class="g-recaptcha" data-sitekey="SUA_CHAVE" data-size="invisible"></div>
```

## 🔍 Monitoramento

### Métricas Importantes
- **Taxa de Resolução**: % de usuários que completam o reCAPTCHA
- **Taxa de Spam**: % de tentativas de spam bloqueadas
- **Tempo de Carregamento**: Impacto na performance do site

### Logs Recomendados
- Tentativas de envio sem reCAPTCHA
- Falhas na validação do reCAPTCHA
- Sucessos no envio do formulário

## 🛡️ Segurança

### Boas Práticas
- ✅ Nunca expor a Secret Key no frontend
- ✅ Validar sempre no backend
- ✅ Implementar rate limiting
- ✅ Monitorar tentativas suspeitas
- ✅ Atualizar chaves periodicamente

### Configurações Avançadas
- **Whitelist de IPs**: Para ambientes corporativos
- **Configurações de Score**: Para reCAPTCHA v3
- **Integração com WAF**: Para proteção adicional

## 📞 Suporte

### Documentação Oficial
- **Google reCAPTCHA**: https://developers.google.com/recaptcha
- **Troubleshooting**: https://developers.google.com/recaptcha/docs/faq

### Problemas Comuns
1. **reCAPTCHA não aparece**: Verificar se a chave está correta
2. **Erro de domínio**: Adicionar domínio nas configurações
3. **Validação falha**: Verificar Secret Key no backend

---

*Esta implementação garante que o formulário de contato da Task AI esteja protegido contra spam e bots, mantendo uma boa experiência do usuário.*
