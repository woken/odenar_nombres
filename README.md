# odenar_nombres
----------------------------
  def order_file_names

    message = "Servicio para ordenar nombres y apellidos Afabeticamente sin importar que se mezclen" 
    status = false 

    path_file = 'tmp/registro.txt'

    name = Array.new 
    lastname = Array.new 
    order_names = Array.new

    if !File.exist?(path_file) then
      message = "No fue posible encontrar la ruta del archivo"
    else 
      file = File.new(path_file, "r")

      file.each do |row| 
      value = row.strip.split(' ') 
      name.push(value[0]) 
      lastname.push(value[1]) 
      end 
      file.close()

      name = name.sort 
      lastname = lastname.sort

      File.open(path_file, 'w') do |f| 
        index = 0 
        while index < name.length
          name_new = name[index] + ' ' + lastname[index]
          f.write("#{name_new}\n")
          index+=1
        end
      end
      status = true 
    end

    data = Hash.new

    response = Hash.new
    response[:status] = status
    response[:code] = 200
    response[:service] = {service_name: 'Api', endpoint:'order_file_names'}
    response[:message] = message
    response[:data] = data
    render Response.new(self.get_response_type, response[:code]).get_response response
  end
-----------------------------
