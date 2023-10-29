import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import okhttp3.ResponseBody;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;

public class WeatherApp {

    public static void main(String[] args) {
        
        String apiKey = "21955c947745726b172511cb7546e33b\\n";
        String city = "New York"; 

        try {
            OkHttpClient client = new OkHttpClient();
            String apiUrl = "https://api.openweathermap.org/data/2.5/weather?q=" + city + "&appid=" + apiKey;
            Request request = new Request.Builder()
                    .url(apiUrl)
                    .build();

            Response response = client.newCall(request).execute();
            ResponseBody responseBody = response.body();
            if (responseBody != null) {
                String jsonData = responseBody.string();
                JSONParser parser = new JSONParser();
                Object obj = parser.parse(jsonData);
                JSONObject json = (JSONObject) obj;

              
                double temperature = Double.parseDouble(json.get("main.temp").toString());
                double humidity = Double.parseDouble(json.get("main.humidity").toString());
                String conditions = ((JSONObject) ((org.json.simple.JSONArray) json.get("weather")).get(0)).get("description").toString();

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
//client.newCall(request).execute(). This sends the request to the OpenWeatherMap API.
//The JSONParser is used to parse the JSON data from jsonData and convert it into a JSON object.


