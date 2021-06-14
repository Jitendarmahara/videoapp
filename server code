#server code
import socket
import cv2
import pickle
import struct ## new

HOST="192.168.43.93"
PORT=10050
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect((HOST,PORT))

data =b""
payload_size = struct.calcsize("H") 
while True:
    while len(data) < payload_size:
        packet = s.recv(4*1024)
        if not packet: break
        data+=packet
    packed_msg_size = data[:payload_size]
    data = data[payload_size:]
    msg_size = struct.unpack("H", packed_msg_size)[0]
    while len(data) < msg_size:
        data += s.recv(4*1024)
    frame_data = data[:msg_size]
    data = data[msg_size:]
    frame = pickle.loads(frame_data)
    cv2.imshow('reciving video',frame)
    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):
        break
s.close()
    
