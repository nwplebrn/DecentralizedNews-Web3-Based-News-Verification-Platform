# DecentralizedNews-Web3-Based-News-Verification-Platform
DecentralizedNews leverages blockchain technology to combat fake news by verifying the authenticity of news articles and rewarding journalists for accurate reporting.
class Block:
    def __init__(self, index, article_hash, verification_status, previous_hash):
        self.index = index
        self.article_hash = article_hash
        self.verification_status = verification_status
        self.previous_hash = previous_hash
        
    def __repr__(self):
        return (f"Index: {self.index}, Article Hash: {self.article_hash}, "
                f"Verified: {self.verification_status}, Previous Hash: {self.previous_hash}")

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.rewards = {}
        
    def create_genesis_block(self):
        return Block(0, "0", True, "0")
    
    def add_block(self, article_hash, verification_status, journalist):
        previous_block = self.chain[-1]
        new_block = Block(len(self.chain), article_hash, verification_status, previous_block.article_hash)
        self.chain.append(new_block)
        self.update_rewards(journalist, verification_status)
        return new_block
    
    def update_rewards(self, journalist, verification_status):
        if journalist not in self.rewards:
            self.rewards[journalist] = 0
        if verification_status:
            self.rewards[journalist] += 1  # Simplified reward mechanism
    
    def get_chain(self):
        return self.chain
    
    def get_rewards(self):
        return self.rewards

# Simulating the platform with a couple of articles
decentralized_news = Blockchain()

# Simulating adding articles
decentralized_news.add_block("hash_article_1", True, "Journalist_1")
decentralized_news.add_block("hash_article_2", False, "Journalist_2")
decentralized_news.add_block("hash_article_3", True, "Journalist_1")

# Displaying the blockchain
print("Blockchain:")
for block in decentralized_news.get_chain():
    print(block)

# Displaying rewards
print("\nRewards:")
print(decentralized_news.get_rewards())
