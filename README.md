import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.text.DecimalFormat;

public class weatherApp {
    public static void main(String[] args) {
        String apiKey = "21955c947745726b172511cb7546e33b";
        String city = "";

        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the name of the city: ");
        city = scanner.nextLine();
        scanner.close();

        try {
            String weatherData = fetchWeatherData(apiKey, city);
            displayWeatherData(weatherData);
        } catch (IOException e) {
            System.out.println("An error occurred: " + e.getMessage());
        }
    }

    public static String fetchWeatherData(String apiKey, String city) throws IOException {
        String baseUrl = "http://api.openweathermap.org/data/2.5/weather?";
        String completeUrl = baseUrl + "appid=" + apiKey + "&q=" + city;
        URL url = new URL(completeUrl);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();

        InputStream inputStream = connection.getInputStream();
        Scanner scanner = new Scanner(inputStream);

        StringBuilder responseData = new StringBuilder();
        while (scanner.hasNext()) {
            responseData.append(scanner.next());
        }

        scanner.close();
        connection.disconnect();

        return responseData.toString();
    }

    public static void displayWeatherData(String weatherData) {
        JsonParser jsonParser = new JsonParser();
        JsonObject jsonObject = jsonParser.parse(weatherData).getAsJsonObject();

        double temperature = jsonObject.getAsJsonObject("main").get("temp").getAsDouble() - 273.15;
        int humidity = jsonObject.getAsJsonObject("main").get("humidity").getAsInt();
        String weatherDescription = jsonObject.getAsJsonArray("weather")
                .get(0).getAsJsonObject().get("description").getAsString();

        DecimalFormat df = new DecimalFormat("#.##");
        String formattedTemperature = df.format(temperature);

        System.out.println("Temperature: " + formattedTemperature + "°C");
        System.out.println("Humidity: " + humidity + "%");
        System.out.println("Weather description: " + weatherDescription);
    }
}
//we create a URL object and open an HttpURLConnection to connect to the API URL. we also specify the request method as GET.
//we use the JSON-Simple library to parse the JSON data into a JSONObject
//extract specific weather information such as temperature, humidity, and conditions from the JSON data.



