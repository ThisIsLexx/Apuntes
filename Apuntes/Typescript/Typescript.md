# Typescript files
---
## Interfaces
Las interfaces son la base de cualquier tipo de objeto que se va a manipular dentro del código. Estas son declaradas con la palabra clave ***interface*** y se implementan de la siguiente manera:
```
interface Clase {
    property1: type,
    property2: type,
    ...
}
```
### Reutilización de tipados o interfaces
Dentro de la declaración de interfaces, se puede hacer uso de la función **export** para poder llamar dentro de cualquier archivo los tipados que sean definidos. Por ejemplo, se puede crear un archivo con tipados para las funciones API, que puedan ser llamados en cualquier service:
***Tipos.ts:***
```
export interface Ejemplo {
    mensaje: string;
}
```
Dentro del archivo donde queremos llamar:
```
import type { Ejemplo } from ~/Tipos.ts

const mensaje = (mensaje: Ejemplo) => {
    return mensaje.mensaje;
}
```
---
## Tipo generico "T"
Dentro de los tipos de datos, para evitar el uso de **any** en las funciones que requieren un cierto grado de reutilización, se emplea el tipado ***generico T***. Este tipado puede recibir parametros esperados como interfaces para hacer uso de las mismas en la función que espera reutilizar código:
```
const fetchData<T>(url: string): Promise<T> {
    try {
        return fetch(url);
    } catch {
        ...
    }
}
```
Esta función puede ser empleada como una función generica para realizar peticiones API. Con el uso de interfaces se puede implementar una limitación en el tipo de datos que se espera obtener:
```
interface ResponseExample {
    code: number,
    message: string,
    response: {
        ...
    }
}

async function fetchExample(url: string): Promise<ResponseExample> {
    return fetchData<ResponseExample>(url);
}
```
