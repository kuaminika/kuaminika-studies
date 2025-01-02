# Typeahead case study

## Functional requirements ( MVP )

- as a searcher, I want to be suggested the top 5 most relavant prefix to avoid typing out everything
   suggestions should be ranked by popularity ( meaning frequency and recency)
- as a searcher I want to type out the first 3 prefix characters. before being pointed out suggestions

## Non functional requirements (Design goals)

CAPELC
consistency (not really needed)
availability extremely needed

favoring latency over consistency.
suggestions are supposed to update based on the speed of keyboard strokes

## Estimations

### Assumptions

google gets 10 Biliion search terms per day
the typeahead is queried an average of 6 times prior a search term => 60 billion typeahead queries per day
a term could be 32 characters long on average
we'd want to keep track of the frequency per term
in the end we're looking at a schema of termFrequency ( term varchar(32), frequency  long)

### Storage calculations

with the assumed schema of how we store termFrequency ( term varchar(32), frequency  long)

- considering that a char is 1 byte, so the term being 32 chars => 32 bytes
- considering that the frequency is a long, then i'd foresee 8 bytes
- we're therefore looking at 40 bytes oer termFrequency

considering that in a day we're dealing with 10 Billion search terms.=> the size we can expect 40 bytes/term *10 billion terms = 400 billion bytes => 400 GB/day
in a year, that's 400 GB*365=146000 GB => 146 TB

- considering that servers usually are 4 TB, sharding will eventually be needed

### read/write heavy

- it is read heavy.
- it's also write heavy but mostly read

## API

updateTermFrequency(term, frequency)
searhTerm(term)

## further discussions

### using Trie

If we are to use a trie, implementing where each node has 36 children.

- each node should store the top 5 suggestions
- each leaf node should store a search term
- implemening updateTermFrequency(term, frequency) would consist of travelling to the node associated to the term and updating the frequency.
  - this implies to then update the ancestor nodes as a frequency change can have an effect on the top 5 suggestions

this will be hard to shard. Lots of skewing

### using hash map

If we are to use a hashmap, we would have two hash maps

- 1 for prefix and their top5 suggestions
- 1 for terms and frequencies

Easier to shard. sharding would be based on term

### latency over consistency

This system is read heavy and write heavy.

however, the writes are expensive as they require to update the top 5 suggestions. this is the reason why sacrificing a few writes for the sake of low latency is ideal.

- we can consider sampling which is to write at every Nth record
- we can consider having a threshold .. meaning that we will update the frequency when the a term has reached a frequency of N.
  - In this case, the search terms will be held in a buffer
