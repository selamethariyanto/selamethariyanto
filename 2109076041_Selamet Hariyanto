import random

# Definisi batasan nilai variabel
min_a = 0
max_a = 30
min_b = 0
max_b = 10
min_c = 0
max_c = 10
min_d = 0
max_d = 10

# Definisi jumlah populasi
pop_size = 6

# Definisi parameter crossover dan mutasi
crossover_rate = 0.8
mutation_rate = 0.1

# Fungsi evaluasi (fitness)
def evaluate(chromosome):
    a = chromosome[0]
    b = chromosome[1]
    c = chromosome[2]
    d = chromosome[3]
    return abs(a + 4*b + 2*c + 3*d -30)

# Inisialisasi populasi secara acak
def initialize_population():
    population = []
    for _ in range(pop_size):
        chromosome = [random.randint(min_a, max_a),
                      random.randint(min_b, max_b),
                      random.randint(min_c, max_c),
                      random.randint(min_d, max_d)]
        population.append(chromosome)
    return population

# Seleksi orang tua berdasarkan probabilitas fitness
def select_parents(population):
    fitness_sum = sum(1 / (1 + evaluate(chromosome)) for chromosome in population)
    probabilities = [(1 / (1 +evaluate(chromosome))) / fitness_sum for chromosome in population]
    cumulative_probabilities = [sum(probabilities[:i+1]) for i in range(len(probabilities))]
    parents = []
    for _ in range(pop_size):
        r = random.random()
        for i in range(pop_size):
            if i == 0 and r < cumulative_probabilities[i]:
                parents.append(population[i])
                break
            elif cumulative_probabilities[i-1] < r < cumulative_probabilities[i]:
                parents.append(population[i])
                break
    return parents

# Crossover dengan metode one-cut point
def crossover(parent1, parent2):
    if random.random() < crossover_rate:
        cut_point = random.randint(1, len(parent1) - 1)
        child1 = parent1[:cut_point] + parent2[cut_point:]
        child2 = parent2[:cut_point] + parent1[cut_point:]
        return child1, child2
    else:
        return parent1, parent2

# Mutasi dengan mengganti satu gen secara acak
def mutate(chromosome):
    if random.random() < mutation_rate:
        gene_to_mutate = random.randint(0, len(chromosome) -1)
        if gene_to_mutate == 0 :
            chromosome[gene_to_mutate] = random.randint(min_a, max_a)
        elif gene_to_mutate == 1:
            chromosome[gene_to_mutate] = random.randint(min_b, max_b)
        elif gene_to_mutate == 2:
            chromosome[gene_to_mutate] = random.randint(min_c, max_c)
        else:
            chromosome[gene_to_mutate] = random.randint(min_d, max_d)
    return chromosome

# Algoritma Genetika
def genetic_algorithm():
    population = initialize_population()
    best_chromosome = None
    best_fitness = float('inf')

    for _ in range(100): # Jumlah Generasi
        parents = select_parents(population)
        next_generation = []
        for i in range(0,len(parents), 2):
            parent1 = parents[i]
            parent2 = parents[i+1] if i+1 < len(parents) else parents[0] # Wraparound crossover
            child1, child2 = crossover(parent1, parent2)
            child1 = mutate(child1)
            child2 = mutate(child2)
            next_generation.extend([child1, child2])

        population = next_generation

        # Evaluasi fitness tiap chromosome dalam populasi
        for chromosome in population:
            fitness = evaluate(chromosome)
            if fitness < best_fitness:
                best_chromosome = chromosome
                best_fitness = fitness

    return best_chromosome

# Menjalankan algoritma genetika untuk mencari solusi
best_solution = genetic_algorithm()
a, b, c, d = best_solution
print(f"Solusi terbaik: a={a}, b={b}, c={c}, d={d}")
print(f"Hasil persamaan: {a} + 4*{b} + 2{c} + 3*{d} = {a + 4*b + 2*c + 3*d}")