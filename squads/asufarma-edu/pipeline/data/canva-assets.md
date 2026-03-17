# Canva Assets — Asufarma

Assets permanentes disponíveis no Canva para uso em designs.
Diana Design deve usar estes asset_ids ao criar designs com generate-design.

## Brand Kit
- **ID:** kAG4986LZbc
- **Nome:** Asufarma

## Produtos (asset_ids)

| Produto | Canva Asset ID | ImgBB URL |
|---------|---------------|-----------|
| Creatina Asufarma sabor Caramelo | MAHEI0n8K1k | https://i.ibb.co/ZRHqWkD5/test.jpg |
| Creatina Asufarma sabor Brigadeiro | MAHEIwkQfZw | https://i.ibb.co/tMmHY6RX/creatina-asufarma-brigadeiro.jpg |
| Maxxy Hair Skin & Nails | (nos uploads do Canva do usuario) | https://i.ibb.co/chPzkFtN/maxxy-hair-skin-nails.jpg |
| DHA Plus Omega3 | (nos uploads do Canva do usuario) | https://i.ibb.co/spJD7WsN/dha-plus-omega3.jpg |
| Nored Fotoprotetor FPS40 | (nos uploads do Canva do usuario) | https://i.ibb.co/Xr42SJpJ/nored-fotoprotetor-fps40.jpg |

## Posts de Referencia (asset_ids)

| Referencia | Canva Asset ID |
|-----------|---------------|
| Melatonina Gummie zzZ (carrossel slide 1) | MAHEIxGcCHQ |
| Colageno Juice Snella (post) | MAHEIy1JjrE |

## Logos (asset_ids)

| Logo | Canva Asset ID |
|------|---------------|
| Logo Horizontal Branco | MAHEI_4xui8 |
| Simbolo Verde Original | MAHEI0ZyxV0 |

## Como Usar

Diana Design deve passar `asset_ids` no parametro de `generate-design`:
```
asset_ids: ["MAHEI0n8K1k"]  // insere a foto da Creatina Caramelo no design
```

Tambem deve sempre usar `brand_kit_id: "kAG4986LZbc"`.

## ImgBB Config
- API Key: configurada em .env (IMGBB_API_KEY)
- Workflow: local file -> ImgBB upload -> HTTPS URL -> Canva upload-asset-from-url

## Arquivos Locais
- Produtos: /Users/admin/Documents/Asufarma/Produtos/
- Logos: /Users/admin/Documents/Asufarma/Branding/logos/
- Simbolos: /Users/admin/Documents/Asufarma/Branding/simbolos/
- Grafismos: /Users/admin/Documents/Asufarma/Branding/grafismos/
- Posts anteriores: /Users/admin/Documents/Asufarma/Posts-Feed/
