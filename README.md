import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class WeatherApp {

    public static void main(String[] args) {

        String apiKey = "21955c947745726b172511cb7546e33b\\n";
        String city = "New York";

        try {
            String apiUrl = "https://api.openweathermap.org/data/2.5/weather?q=" + city + "&appid=" + apiKey;

            URL url = new URL(apiUrl);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");

            int responseCode = connection.getResponseCode();
            if (responseCode == 200) {
                BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String inputLine;
                StringBuilder content = new StringBuilder();
                while ((inputLine = in.readLine()) != null) {
                    content.append(inputLine);
                }
                in.close();

                JSONParser parser = new JSONParser();
                JSONObject json = (JSONObject) parser.parse(content.toString());


                double temperature = Double.parseDouble(json.get("main.temp").toString());
                double humidity = Double.parseDouble(json.get("main.humidity").toString());
                JSONArray weatherArray = (JSONArray) json.get("weather");
                String conditions = ((JSONObject) weatherArray.get(0)).get("description").toString();

                System.out.println("Weather in " + city);
                System.out.println("Temperature: " + temperature + "°C");
                System.out.println("Humidity: " + humidity + "%");
                System.out.println("Conditions: " + conditions);
            } else {
                System.out.println("Error fetching weather data.");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
//we create a URL object and open an HttpURLConnection to connect to the API URL. we also specify the request method as GET.
//we use the JSON-Simple library to parse the JSON data into a JSONObject
//extract specific weather information such as temperature, humidity, and conditions from the JSON data.



