# file-request-raspberry

def file_request_raspberry(HOSTS):
    print("Richiesta file raspberry")
    output_messages = ""  # Stringa per memorizzare i messaggi di output
    status_file = [] # Matrice per memorizzare lo stato per ogni host
    try:
        for host in HOSTS:  # Itera su ogni host nella lista HOSTS
            with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
                s.connect((host, PORT))
                print(f"Connesso al server {host}:{PORT}")
                output_messages += f"Connesso al server {host}:{PORT}\n"
                s.sendall(b'SEND FILE')
                file_path = SAVE_PATH + f'received_file_{host}.txt' #nome che viene dato al file quando viene ricevuto
                with open(file_path, 'wb') as f:
                    while True: 
                        data = s.recv(1024)
                        if not data:
                            break
                        f.write(data)
                print(f'File ricevuto e salvato con successo su {file_path}')
                output_messages += f'File ricevuto e salvato con successo su {file_path}\n'
                status = 1 # se ricevo il file, dizionario
                status_file.append([host,status])
                
    except Exception as e:
        print(f"Errore durante la richiesta del file da {HOSTS}: {e}")
        output_messages += f"Errore durante la richiesta del file da {HOSTS}: {e}\n"
        status = 0
        status_file.append([host,status])
    return status_file #,output_messages
    print(status)


## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with React and Chakra UI.

- Vite
- React
- Chakra UI

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/file-request-raspberry.git
cd file-request-raspberry
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
