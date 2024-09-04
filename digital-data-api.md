
### 📊 **@digital/data-api**

Esta API oferece acesso a dados de séries temporais, informações sobre os ativos e métricas associadas. Possui três endpoints principais:

1. **`/api/data`**: Consultar dados de séries temporais.  
2. **`/api/data/assets`**: Listar ativos cadastrados.  
3. **`/api/data/assets/{id}`**: Obter detalhes específicos de um ativo.

---

#### **1. `/api/data`** - Consultar Dados de Séries Temporais

**Método:** `GET`

**Parâmetros de Consulta**

- **Requeridos**  
- `source` - Origem dos dados (`dataset`, `timeseries`)  
- `resource` - Nome do recurso  
- `period` - Período dos dados (`this_year`, `[start_date,finish_date]` em formato ISO Date Time)  
- `resample` - Frequência de amostragem (`minute`, `hour`, `day`, `week`, `month`)

- **Opcionais**  
- `columns` - Lista de colunas específicas (`array` ou `null` para incluir todas)  
- `layout` - Formato do layout dos dados (`column` ou `raw`)  
- `include_metadata` - Incluir metadados (`true` ou `false`)  
- `columns_config` - Configuração personalizada das colunas (`object` ou `null`)  
- `include_statistics` - Incluir estatísticas (`true` ou `false`)  
- `apply_filter` - Aplicar filtros (`true` ou `false`)

**Exemplos de Requisição**

- `GET /api/data?source='dataset'&resource='test esp sparse'&period=['2024-09-04T03:00:00.000Z','2024-09-05T02:59:59.999Z']&resample='minute'`  
- `GET /api/data?source='timeseries'&resource='EAF 2'&period=['2024-09-04T03:00:00.000Z','2024-09-05T02:59:59.999Z']&resample='hour'&columns=['LP steam consumption','NG consumption']&layout='raw'`

---

#### **2. `/api/data/assets`** - Listar Ativos

**Resposta**  
```json  
[  
  {  
    "id": "number",  
    "name": "string",  
    "description": "string",  
    "profile": "string"  
  }  
]  
```

---

#### **3. `/api/data/assets/{id}`** - Detalhes de um Ativo

**Método:** `GET`

**Parâmetros de Consulta**

- `include_metrics` - Incluir métricas (`true` ou `false`)  
- `include_datasets` - Incluir conjuntos de dados (`true` ou `false`)

**Exemplo de Requisição**

- `GET /api/data/assets/12345?include_metrics=true&include_datasets=true`

**Resposta**  
```json  
{  
	"id": "number",  
	"name": "string",  
	"description": "string",  
	"profile": "string",  
	"metrics": [  
		{  
			"id": "number",  
			"name": "string",  
			"description": "string",  
			"status": "string",  
			"type": "string",  
			"sampling": "string",  
			"layer": "string",  
			"unit_symbol": "string",  
			"aggregator": "string",  
			"timeseries": "array"  
		}  
	],  
	"datasets": [  
		{  
			"id": "number",  
			"name": "string",  
			"description": "string",  
			"type": "string",  
			"cycle_metric": "string",  
			"filter": "string",  
			"columns": [  
				{  
					"id": "number",  
					"alias": "string",  
					"asset": "string",  
					"profile": "string",  
					"metric": "string",  
					"data_type": "string",  
					"unit_symbol": "string",  
					"layer": "string",  
					"aggregator": "string"  
				}  
			]  
		}  
	]  
}
```
