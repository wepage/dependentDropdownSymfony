# dependentDropdownSymfony
Symfony 6 Dependent Dropdowns from database using ajax for dynamicaly loading second dropdown
# form can be used for creating new entity entry and for editing existing entry, it will select the values firstry been selected

#Need a endpoint to post ajax to get json responce with the cities by country 
        $cities = json_decode($this->serializer->serialize($this->citiesRepo->citiesByCountry($country), 'json'), true);
        return new JsonResponse($processes);
         // e.g
        // [{"id":"3","name":"Rousse"},{"id":"4","name":"Sofia"}]

AJAX EXAMPLE
<script>
        $('#form_country').change(function() {
            let country = $(this);
            // get cities by country
            if(country){
                $.ajax({
                    url: "/ajax/citiesByCountry/"+country.val(),
                    type: "GET",
                    dataType: "JSON",
                    success: function (jsonResponceCities) {
                        let city_select = $("#form_city");
                        // Remove current options
                        city_select.html('');
                        // Empty value ...
                        city_select.append('<option value> Select a city of ' + country.find("option:selected").text() + ' ...</option>');
                        $.each(jsonResponceCities, function (key, city) {
                            city_select.append('<option value="' + city.id + '">' + city.name + '</option>');
                        });
                    },
                    error: function (err) {
                        alert("An error ocurred while loading data ...");
                    }
                });
            }
        });
    </script>
