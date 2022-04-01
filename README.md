# Bitcoin-Mining-in-Blockchain
from hashlib import sha256

Max_NONCE = 1000000000

def SHA256(text):
    return sha256(text.encode('ascii')).hexdigest()

def mine(block_number, transaction, previous_hash, prefix_zeros):
    prefix_str = '0'* prefix_zeros
    
    for nonce in range(Max_NONCE):
        text = str(block_number) + transaction + previous_hash + str(nonce)
        new_hash = SHA256(text)
        
        if new_hash.startswith(prefix_str):
            
            print(f'Yey ! Successfully mined bitcoin with nonce value:{nonce}')
            
            return new_hash
        
    raise BaseException(f"could't find after a trying {Max_NONCE} times")
    
if __name__ == '__main__':
    transaction = '''
    Shubham -> Arati -> 20
    Varsha -> Monu ->45
    '''
    
    difficulty = 4 #try changing this to higher number and you will see it will take more time for mining as difficulty increases
    import time    
    start = time.time()
    print("start mining")
    new_hash = mine(5,transaction,
            'b5d4045c3f466fa91fe2cc6abe79232a1a57cdf104f7a26e716e0a1e2789df78',
            difficulty)
    total_time = str((time.time() - start))
    print(f" End mining. Mining took: {total_time} seconds")
    print(new_hash)
        
