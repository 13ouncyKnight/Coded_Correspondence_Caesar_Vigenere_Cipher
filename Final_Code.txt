#Step 1: To decode an encrypted message, the encrypted letters' index should be shifted to the right
alphabet = "abcdefghijklmnopqrstuvwxyz"
def caesar_decode(message, offset):
  original_message = ""
  for letter in message:
      if letter in alphabet:
        character_index = alphabet.find(letter)
        original_message += alphabet[(character_index + offset) % 26]
      else:
        original_message += letter
  print(original_message)      
  return original_message

#caesar_decode("jxu evviuj veh jxu iusedt cuiiqwu yi vekhjuud.", 10)

#To encode a message, shift the message's letters to the left with the offset
def caesar_encode(message, offset):
  decoded_message = ""
  for letter in message:
      if letter in alphabet:
        character_index = alphabet.find(letter)
        decoded_message += alphabet[(character_index - offset) % 26]
      else:
        decoded_message += letter
  print(decoded_message)      
  return decoded_message

caesar_decode("jxu evviuj veh jxu iusedt cuiiqwu yi vekhjuud.", 10)
caesar_decode("bqdradyuzs ygxfubxq omqemd oubtqde fa oapq kagd yqeemsqe ue qhqz yadq eqogdq!", 14)
#Brute force the encrypted message: The encrypted message should be shifted to the right so the condition is to replace each letter index with an index of the alphabet shifted to the right
def brute_force_decode(message): 
  for n in range(0, 27):
    decoded_message = ""
    for letter in message:      
      if letter in alphabet:
        character_index = alphabet.find(letter)
        decoded_message += alphabet[(character_index + n) % 26]
      else:
        decoded_message += letter   
    print("Offset ", n, ":\n", decoded_message)
    n +=1        

#brute_force_decode("bqdradyuzs ygxfubxq omqemd oubtqde fa oapq kagd yqeemsqe ue qhqz yadq eqogdq!")    

#brute_force_decode("vhfinmxkl atox kxgwxkxw tee hy maxlx hew vbiaxkl hulhexmx. px'ee atox mh kxteer lmxi ni hnk ztfx by px ptgm mh dxxi hnk fxlltzxl ltyx.")

#####VIGENERE CIPHER CODE
coded_message = "txm srom vkda gl lzlgzr qpdb? fepb ejac! ubr imn tapludwy mhfbz cza ruxzal wg zztylktoikqq!"

keyword = "friends"

#To decode vigenere, create a function that accepts two arguments coded_message and keyword: iterate through each letter in keyword and for each letter in coded_message, append the letters in keyword over and over again.
#Encode
def encode_vigenere(message, keyword):
  key_phrase = ""
  key = 0
  for letter in message:
    key_len = len(keyword)     
    if letter in alphabet:    
      coded_letter = keyword[(key%key_len)]
      key_phrase += coded_letter
      key+=1
    else:
      key_phrase += letter   
  ciphered_message = ""
  for i in range(len(message)):  
    if message[i] in alphabet:    
      letter_index = alphabet.find(message[i])
      key_index = alphabet.find(key_phrase[i])
      ciphered_message += alphabet[(letter_index - key_index) % 26 ]
    else:
      ciphered_message += key_phrase[i]
  return ciphered_message
#decode
def decode_vigenere(message, keyword):
  key_phrase = ""
  key = 0
  for letter in message:
    key_len = len(keyword)     
    if letter in alphabet:       
      coded_letter = keyword[(key%key_len)]
      key_phrase += coded_letter
      key+=1
    else:
      key_phrase += letter   
  ciphered_message = ""
  for i in range(len(message)):  
    if message[i] in alphabet:    
      letter_index = alphabet.find(message[i])
      key_index = alphabet.find(key_phrase[i])
      ciphered_message += alphabet[(letter_index + key_index) % 26 ]
    else:
      ciphered_message += key_phrase[i]   
  return ciphered_message
#Decode  
def vigenere_decode(message, keyword):
  keyword_phrase = ""
  keyword_index = 0    
  for letter in message:
    if keyword_index >= len(keyword):
      keyword_index = 0
    if letter in alphabet:
      keyword_phrase += keyword[keyword_index]
      keyword_index +=1
    else:
      keyword_phrase += letter 
  decoded_message = ""   
  for i in range(len(message)):
    if message[i] in alphabet:
      old_letter_index = alphabet.find(message[i])
      offset_index = alphabet.find(keyword_phrase[i])
      new_letter = alphabet[(old_letter_index + offset_index) % 26]  
      decoded_message += new_letter
    else:
      decoded_message += message[i]
  return decoded_message    
#Encode   
def vigenere_encode(message, keyword):
  keyword_phrase = ""
  keyword_index = 0    
  for letter in message:
    if keyword_index >= len(keyword):
      keyword_index = 0
    if letter in alphabet:
      keyword_phrase += keyword[keyword_index]
      keyword_index +=1
    else:
      keyword_phrase += letter 
  encrypted_message = ""   
  for i in range(len(message)):
    if message[i] in alphabet:
      old_letter_index = alphabet.find(message[i])
      offset_index = alphabet.find(keyword_phrase[i])
      new_letter = alphabet[(old_letter_index - offset_index) % 26]  
      encrypted_message += new_letter
    else:
      encrypted_message += message[i]
  return encrypted_message  

print("\n==========THE VIGENERE CIPHER: ==========")  
ciphered_vigenere = encode_vigenere("barry is the spy", "dog")
print("Decoded Message: ",decode_vigenere("ymlok cp fbb ejv", "dog"))
print("Encrypted Message: ",ciphered_vigenere)

vigenere_message = """ymlok cp fbb ejv
"""
vigenere_keyword = "dog"

print(decode_vigenere(vigenere_message, vigenere_keyword))

vigenere_keyword = "eminem"

print("Encoding Message: \t",encode_vigenere("""My tea's gone cold, I'm wondering why I got out of bed at all
The morning rain clouds up my window and I can't see at all
And even if I could it'll all be grey, but your picture on my wall
It reminds me, that it's not so bad, it's not so bad
My tea's gone cold, I'm wondering why I got out of bed at all
The morning rain clouds up my window and I can't see at all
And even if I could it'll all be gray, but your picture on my wall
It reminds me, that it's not so bad, it's not so bad""", vigenere_keyword))

print("\nOriginal Message: \t",decode_vigenere("""Mu hwn'o ukbw pkzz, I'a objrafaac kdm I ybp cqh gs xsz ol nhz
Tds ebnbeby ewwj qdbqro ih zu kebvbs ojr I unj'h osw np ohz
Afq ajab as I ycqzv vp'zh ody xs cfwl, xip mghn deqlhns kb el sohz
Il eaaebvf is, pvsg eh'o bgg oc xov, vp'g jcl fk pwr
Mq gao'o ugaa qkzv, I'z scjrweebc kzl I ccp cmg kt xsv np ohz
Tzr icnbaac fwwf phcqrk hl au kaazcs ofq I yoj'h kra op ody
Ajr ajwa et I ycmyz wp'zd nhz xs yewm, xil lkin dappins ga im sody
Ip faaaazg is, luwh eh'k akh oc tnz, wp'g fbp gk psq""", vigenere_keyword))

print("\n")

print(decode_vigenere("i surrender all, o to thee, my blessed saviour, i surrender all", "holy spirit"))
print(encode_vigenere("p gfpqwclvz tsz, z rn lwmv, ur izpqrws ardbvic, g rmgzvvwlf ljk", "holy spirit"))

print("\n")

print(decode_vigenere("txm srom vkda gl lzlgzr qpdb? fepb ejac! ubr imn tapludwy mhfbz cza ruxzal wg zztylktoikqq!", "friends"))
print(encode_vigenere(decode_vigenere("txm srom vkda gl lzlgzr qpdb? fepb ejac! ubr imn tapludwy mhfbz cza ruxzal wg zztylktoikqq!", "friends"), "friends"))