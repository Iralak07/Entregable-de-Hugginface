# Entregable-de-Hugginface



## Proyecto 1 : Utilizando un api de hugginface de un modelo llm crea una aplicación donde el usuario pueda realizar preguntas y el modelo le responda, en el readme especifica el modelo usado y los parámetros en la petición junto con un ejemplo de uso.

Paso 1: Configuración inicial

Necesitaremos:

    Una cuenta en Hugging Face.

    Una API Key de Hugging Face. Para obtenerla:
        Ve a tu perfil en Hugging Face.
        Accede a la sección "Settings" > "Access Tokens".
        Genera un nuevo token y copia su valor.

    Elegir un modelo LLM (Language Model). Para este proyecto, usaremos el modelo Qwen/QwQ-32B-Preview.


Paso 2: Código para interactuar con la API

El siguiente código configura la interacción con el modelo LLM a través de la API de Hugging Face. 

    from huggingface_hub import InferenceClient
    
    client = InferenceClient(api_key="hf_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx")
    
    messages = [
    	{
    		"role": "user",
    		"content": "What is the capital of France?"
    	}
    ]
    
    completion = client.chat.completions.create(
        model="Qwen/QwQ-32B-Preview", 
    	messages=messages, 
    	max_tokens=500
    )

    print(completion.choices[0].message)

Ejemplo de uso:

![Screenshot from 2025-01-06 20-50-20](https://github.com/user-attachments/assets/41b10139-3f11-41d7-be3f-f76e4515d80f)

Respuesta:

![Screenshot from 2025-01-06 20-55-35](https://github.com/user-attachments/assets/68bbc581-e927-4b38-9abe-cc0b39550dee)



## Proyecto 2:

Paso 1: Configuración del Entorno

    Requisitos:
        Tener instalada la librería huggingface_hub para interactuar con la API.
        Una clave API válida de Hugging Face (se puede obtener en tu cuenta de Hugging Face).

Paso 2: Creación de la Clase ModelManager

La clase ModelManager se diseñó para manejar las siguientes tareas:

    def __init__(self, api_key, models):
        self.client = InferenceClient(api_key=api_key)
        self.models = models
        self.current_model_index = 0
        
Cambio de Modelo (switch_model):

    Cambia al siguiente modelo en la lista.
    Si llega al final de la lista, vuelve al inicio utilizando el operador módulo (%).
    Imprime el nombre del modelo actual para referencia.

Obtención del Modelo Actual (get_current_model):

    Devuelve el nombre del modelo que está activo en ese momento.

    def get_current_model(self):
      return self.models[self.current_model_index]

Consulta al Modelo (chat):

    Recibe una lista de mensajes estilo conversación.
    Selecciona el modelo actual y realiza una consulta a través de la API.
    Devuelve la respuesta generada por el modelo.


    def chat(self, messages, max_tokens=500):
      model = self.get_current_model()
      print(f"Consultando el modelo: {model}", end='\n\n')
      response = self.client.chat.completions.create(
          model=model,
          messages=messages,
          max_tokens=max_tokens
      )
      return response.choices[0].message


Paso 3: Ejecución del Proyecto
Configuración Inicial

    Se definieron los modelos que se utilizarán:
        Qwen/QwQ-32B-Preview
        microsoft/Phi-3.5-mini-instruct
    Se creó una instancia de la clase ModelManager con la clave API y los modelos.

Interacción con los Modelos

    Primer Modelo:
        Se envió una pregunta: "¿Cuál es la comida típica de Colombia?".
        El primer modelo (Qwen/QwQ-32B-Preview) generó una respuesta.

      messages = [{"role": "user", "content": "¿Cuál es la comida típica de Colombia?"}]
      response = manager.chat(messages)
      print(response.content)


Cambio de Modelo:

    Se alternó al siguiente modelo en la lista utilizando switch_model.

    manager.switch_model()

Segundo Modelo:

    Se volvió a enviar la misma pregunta al segundo modelo (microsoft/Phi-3.5-mini-instruct).
    Se imprimió la respuesta generada.


Ejemplo realizado:

  
![Screenshot from 2025-01-06 21-56-45](https://github.com/user-attachments/assets/3219ba61-89d7-48ce-a381-4ce7bf9e01c7)
![Screenshot from 2025-01-06 21-57-06](https://github.com/user-attachments/assets/9fcfcbd2-f84f-44e9-8ea2-84703e32de58)
![Screenshot from 2025-![Screenshot from 2025-01-06 21-57-28](https://github.com/user-attachments/assets/606a3dc1-aec8-47b0-8620-f3caa8ad6095)
01-06 21-57-18](https://github.com/user-attachments/assets/0ec158c0-4854-4c62-bf0a-8e18dd3612d0)
![Screenshot from 2025-01-06 21-57-38](https://github.com/user-attachments/assets/925f35fd-95f3-4762-8127-f1d31f6d507e)

  
## Diagrama de flujo

![Screenshot from 2025-01-06 21-55-52](https://github.com/user-attachments/assets/78ea8407-c6f1-4f27-a877-c6008636f17a)


