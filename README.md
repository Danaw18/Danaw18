import java.util.HashMap;
import java.util.Map;

class WeatherData {
    private double temperature;
    private int humidity;
    private double windSpeed;
    private String conditions;

    public WeatherData(double temperature, int humidity, double windSpeed, String conditions) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.windSpeed = windSpeed;
        this.conditions = conditions;
    }

    public double getTemperature() {
        return temperature;
    }

    public int getHumidity() {
        return humidity;
    }

    public double getWindSpeed() {
        return windSpeed;
    }

    public String getConditions() {
        return conditions;
    }




}


class WeatherDataAdapter {

    public WeatherData convertDataFromExternalAPI(Map<String, Object> externalData) {

        double temperature = (double) externalData.get("temp");
        int humidity = (int) externalData.get("humidity");
        double windSpeed = (double) externalData.get("wind_speed");
        String conditions = (String) externalData.get("weather_condition");


        WeatherData weatherData = new WeatherData(temperature, humidity, windSpeed, conditions);

        return weatherData;
    }
}

public class ssss {
    public static void main(String[] args) {

        Map<String, Object> externalData = new HashMap<>();
        externalData.put("temp", 25.5);
        externalData.put("humidity", 60);
        externalData.put("wind_speed", 10.2);
        externalData.put("weather_condition", "sunny");


        WeatherDataAdapter adapter = new WeatherDataAdapter();
        WeatherData standardizedData = adapter.convertDataFromExternalAPI(externalData);


        System.out.println("Temperature: " + standardizedData.getTemperature());
        System.out.println("Humidity: " + standardizedData.getHumidity());
        System.out.println("Wind Speed: " + standardizedData.getWindSpeed());
        System.out.println("Conditions: " + standardizedData.getConditions());
    }
}

    //convertDataFromExternalAPI  method that converts data from an external API into a standardized format
