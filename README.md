public class ass4 {
    public static void main(String[] args) {
        WeatherAdapterAPI1 api1 = new WeatherAdapterAPI1();
        WeatherAdapterAPI2 api2 = new WeatherAdapterAPI2();

        WeatherData data1 = api1.fetchAndConvertData();
        WeatherData data2 = api2.fetchAndConvertData();

        System.out.println("Weather Data from API 1:");
        System.out.println("Temperature: " + data1.getTemperature() + "°C");
        System.out.println("Humidity: " + data1.getHumidity() + "%");
        System.out.println("Wind Speed: " + data1.getWindSpeed() + " km/h");
        System.out.println("Conditions: " + data1.getConditions());
        System.out.println("Location: " + data1.getLocation() + "\n");

        System.out.println("Weather Data from API 2:");
        System.out.println("Temperature: " + data2.getTemperature() + "°C");
        System.out.println("Humidity: " + data2.getHumidity() + "%");
        System.out.println("Wind Speed: " + data2.getWindSpeed() + " km/h");
        System.out.println("Conditions: " + data2.getConditions());
        System.out.println("Location: " + data2.getLocation());
    }
}

class WeatherData {
    private double temperature;
    private int humidity;
    private double windSpeed;
    private String conditions;
    private String location;

    public WeatherData(double temperature, int humidity, double windSpeed, String conditions, String location) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.windSpeed = windSpeed;
        this.conditions = conditions;
        this.location = location;
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

    public String getLocation() {
        return location;
    }

}

class WeatherAdapterAPI1 {
    public WeatherData fetchAndConvertData() {
        double temp = 25.5;
        int humidity = 60;
        double wind = 10.2;
        String weather = "Clear";
        String city = "New York";

        return new WeatherData(temp, humidity, wind, weather, city);
    }
}

class WeatherAdapterAPI2 {
    public WeatherData fetchAndConvertData() {
        double temp = 30.5;
        int humidity = 55;
        double wind = 14.3;
        String weather = "Partly Cloudy";
        String city = "Los Angeles";

       
        return new WeatherData(temp, humidity, wind, weather, city);
    }
}




Weather Data is a class representing the standardized format for weather data, with fields for temperature, humidity, wind speed, weather conditions, and location.

Weather Adapter API 1 simulates fetching data from the first fictional API and converting it into the standardized format.

Weather Adapter API 2 simulates fetching data from the second fictional API and converting it into the standardized format.

In the main method, i am  create instances of Weather Adapter API 1 and Weather Adapter API 2, fetch and convert data from these APIs, and then print the weather information for each API.
