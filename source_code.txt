#Part 1 - was not able to properly decrpyt the code
#Very randomized decrpytions too
import random
import string

# Define the encrypted phrases
phrases = [
    "nyyfp jxflw jfyij fqtkg wfajw dytxy fsizu yttzw jsjrn jxgzy ozxyf xrzhm ytxyf sizuy ttzwk wnjsi x",
    "skses faexd wkzsf vtdgg vausf twayf gjwva usftw vwklj gqwvt mlsks kqetg dsksk qetgd ausft wafug jjmhl atdwa usftw wnwjd sklaf y",
    "nfrdf rqqfl abfoj fdfsy orcsy xrcwz hrbdf qxfms qsyyk djyhy dfoof rorho cfszs qjykb oafhy sfosj rszhs jflzo qsywy kdqyd dynsj zqofr sjsrg fqxbr mfzhs jfqjr oynyw hfnbz wfsjf qkhdz qfywr hfnny dborn ydbos jrsyk dafby ufomy ldrof erufj zqbzw fsyxd ysfms rhohy kdzqj jfozo hyswf fbsjz qqrmd zwzmf rurzh ydflx scyhf rhonf nzbbh ysofa rsfjz qxdyw ykhon zqoyl rssjf qfxdy mffoz heqyw lcwdz fhozm rhyhb cqrcs jzqyw rbbsj fqykb qzjru ffhmy khsfd fozhl csdru fbqjz qnrqs jflyq sjklr h",
    "sdfwd ridss dfwsx nsels xwkgw lsedi uxwsx wrsel idfcw reisx wveit sdlgj jwrsx wlcei plnit nrrdu ldjdg srnpw dgljd rsgiw drsds nqwnr vlnpn eilsn lwndj srdgf cwlni tfhdz zdlei pwits xwvsd tewsd lcwwz idvdr wnitf hnlcw wzsdl nhuww itsxw xwnrs nyxwn itsxw sxdgl nitin sgrnc lxdyq lsxns jcwlx elxwe rsdse lnydi lgvvn sedit wmdgs chsdf wuelx"
]


def generate_key():
    # Generate a random substitution key
    alphabet = list(string.ascii_lowercase)
    shuffled_alphabet = random.sample(alphabet, len(alphabet))
    key = dict(zip(alphabet, shuffled_alphabet))
    return key


def decrypt(ciphertext, key):
    # Decrypt the ciphertext using the given key
    return ''.join(key.get(char, char) for char in ciphertext)


def fitness(plaintext, target):
    # Simple fitness function - count matching characters
    return sum(1 for a, b in zip(plaintext, target) if a == b)


def genetic_algorithm(ciphertext, generations=1000, population_size=100, print_interval=100):
    target_length = len(ciphertext)
    target = ' ' * target_length  # Assume spaces for the target text

    # Initialize population with random keys
    population = [generate_key() for _ in range(population_size)]

    # Initialize best_solution before the loop
    best_solution = ""

    for generation in range(generations):
        # Evaluate fitness for each individual
        fitness_scores = [(individual, fitness(decrypt(ciphertext, individual), target)) for individual in population]

        # Sort individuals by fitness
        fitness_scores.sort(key=lambda x: x[1], reverse=True)

        # Select the top individuals to be parents
        parents = [individual for individual, _ in fitness_scores[:int(population_size * 0.2)]]

        # Crossover: Create new individuals by combining parents
        children = []
        for _ in range(population_size - len(parents)):
            parent1, parent2 = random.sample(parents, 2)
            crossover_point = random.randint(1, target_length - 1)
            child = {char: parent1[char] if i < crossover_point else parent2[char] for i, char in enumerate(string.ascii_lowercase)}
            children.append(child)

        # Mutate: Introduce random changes to some individuals
        for child in children:
            if random.random() < 0.1:
                char1, char2 = random.sample(string.ascii_lowercase, 2)
                child[char1], child[char2] = child[char2], child[char1]

        # Replace the old population with the new one
        population = parents + children

        # Print the best solution every print_interval generations
        if (generation + 1) % print_interval == 0:
            best_solution = decrypt(ciphertext, fitness_scores[0][0])
            print(f"Generation {generation + 1}, Best Solution: {best_solution}")

        # Check if we have found the solution
        if best_solution == target:
            print("Decryption successful!")
            break

    # Return the best decryption key found
    return fitness_scores[0][0]


# Apply the genetic algorithm to each encrypted phrase
for index, phrase in enumerate(phrases, start=1):
    print(f"\nDecrypting Phrase {index}:")
    best_key = genetic_algorithm(phrase, print_interval=100)
    decrypted_text = decrypt(phrase, best_key)
    print(f"\nDecrypted Text: {decrypted_text}\n")

#Part 2
def substitution_encrypt(plain_text, key):
    # Ensure that the plain text only contains alphabetic characters
    plain_text = ''.join(char for char in plain_text if char.isalpha() or char.isspace())

    # Create a dictionary to map each letter to its substitution
    substitution_dict = dict(zip('abcdefghijklmnopqrstuvwxyz ', key.lower() + ' '))

    # Encrypt the plain text using the substitution dictionary
    encrypted_text = ''.join(substitution_dict.get(char, char) for char in plain_text.lower())
    return encrypted_text

def substitution_decrypt(encrypted_text, key):
    # Create a dictionary to map each substitution back to its original letter
    substitution_dict = dict(zip(key.lower() + ' ', 'abcdefghijklmnopqrstuvwxyz '))

    # Decrypt the encrypted text using the substitution dictionary
    decrypted_text = ''.join(substitution_dict.get(char, char) for char in encrypted_text.lower())
    return decrypted_text

def main():
    while True:
        print("\nMenu:")
        print("1. Encrypt")
        print("2. Decrypt")
        print("3. Exit")

        choice = input("Please choose an option (1/2/3): ")

        if choice == '1':
            plaintext = input("Enter the text to encrypt: ")
            key = input("Enter the modified alphabet key: ")
            encrypted_text = substitution_encrypt(plaintext, key)
            print("Encrypted text:", encrypted_text)

        elif choice == '2':
            encrypted_text = input("Enter the text to decrypt: ")
            key = input("Enter the modified alphabet key: ")
            decrypted_text = substitution_decrypt(encrypted_text, key)
            print("Decrypted text:", decrypted_text)

        elif choice == '3':
            print("Exiting the program. Goodbye!")
            break

        else:
            print("Invalid choice. Please enter 1, 2, or 3.")

if __name__ == "__main__":
    main()
