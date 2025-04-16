import requests

# Configura tus credenciales
url = "https://api-football-v1.p.rapidapi.com/v3/fixtures?live=all"

headers = {
    "x-rapidapi-key": "64c6d6718528cd26f686375dff92fbcb",
    "x-rapidapi-host": "api-football-v1.p.rapidapi.com"
}

try:
    response = requests.get(url, headers=headers)
    data = response.json()

    if "response" not in data:
        print("Error en la respuesta:", data)
    else:
        print("Conexión exitosa. Analizando partidos en vivo...\n")
        partidos = data["response"]

        for partido in partidos:
            teams = partido["teams"]
            stats = partido.get("statistics", [])
            fixture = partido["fixture"]

            home_team = teams["home"]["name"]
            away_team = teams["away"]["name"]
            score_home = partido["goals"]["home"]
            score_away = partido["goals"]["away"]
            status = fixture["status"]["long"]

            # Aquí podrías extraer datos más precisos si están disponibles:
            # Por ahora, simplemente mostramos la información básica
            print(f"{home_team} {score_home} - {score_away} {away_team} | {status}")

except Exception as e:
    print("Ocurrió un error al intentar acceder a la API:", e)
