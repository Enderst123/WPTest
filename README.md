#Trying to write an if / else statement that puts "no Address found" when "current_addresses" is empty

#The Script:

nestedArray = [
[ "First Middle LastName", "City", "State", "Zip" ]
]
uri = URI('https://proapi.whitepages.com/3.0/person')

nestedArray.each do|pers|
  params = {
    'api_key'  => 'PersonalAPIKeyCOde',
    'name' => pers[0],
    'address_city' => pers[1],
    'address.state_code' => pers[2],
    'address.postal_code' => pers[3],
    'address.country_code' => 'United States',
    'format' => 'JSON',
  }
  uri.query = URI.encode_www_form(params)
  response_hash = JSON.parse(open(uri).read)
  # puts response_hash
  if response_hash['count_person'] == nil
    puts pers[0] + " - No address found."
  elsif response_hash['count_person'] == 0        
    puts pers[0] + " - No address found."
  elsif response_hash['current_addresses'] = [].empty?
    puts pers[0] + " - No address found."  
  else
    puts response_hash['person'][0]['name'] + "|" + response_hash['person'][0]['current_addresses'][0]['street_line_1'] + "|" + response_hash['person'][0]['current_addresses'][0]['city'] + ", " + response_hash['person'][0]['current_addresses'][0]['state_code'] + " " + response_hash['person'][0]['current_addresses'][0]['postal_code']
  end
end

#The Response:

{
  "count_person": 18,
  "person": [
    {
      "id": "Person.4d9c85bd-27ec-4576-b77f-7be02cbbf2be",
      "name": "Fake Name",
      "firstname": "First",
      "middlename": "Middle",
      "lastname": "Last",
      "age_range": null,
      "gender": null,
      "found_at_address": {
        "id": "WhitepagesIDNUMBERSEQUENCE",
        "location_type": "Address",
        "street_line_1": "Secret Address",
        "street_line_2": null,
        "city": "Wirtz",
        "postal_code": "*****",
        "zip4": "4043",
        "state_code": "**",
        "country_code": "US",
        "lat_long": {
          "latitude": 00.000000,
          "longitude": -00.000000,
          "accuracy": "RoofTop"
        },
        "is_active": true,
        "delivery_point": "SingleUnit",
        "link_to_person_start_date": "2017-05-03",
        "link_to_person_end_date": null
      },
      "current_addresses": [

      ],
      
     # The API breaks because  "current_addresses" is empty
     my attempt has included 
     elsif response_hash['current_addresses'] = [].empty?
    puts pers[0] + " - No address found."  
     elsif response_hash['current_addresses'] = nil
    puts pers[0] + " - No address found." 
    
    both of these let the API continue but they mark all addresses as "No Address Found"
      
      
