# Normalization-of-Property-Data-Using-Edit-Distance-and-Word-Embedding.
![image](https://github.com/user-attachments/assets/5f37a08e-303d-4335-a46b-9d10505e804a)

# I) Theoretical Foundation and Research Process

## **1. Levenshtein Distance**

Levenshtein Distance, also known as Edit Distance, is a critical method for measuring the difference between two character sequences. In the context of the Smart Urban Project, this method can be effectively applied to standardize cadastral data, which often includes complex information such as street names, areas, and addresses. These data are prone to errors or inconsistencies during entry, such as typos, abbreviations, or differing character usage, reducing data accuracy.

\[
lev_{a,b}(i,j) = 
\begin{cases} 
\max(i, j) & \text{if } \min(i, j) = 0 \\ 
\min \left\{
\begin{matrix}
lev_{a,b}(i-1,j)+1 \\ 
lev_{a,b}(i,j-1)+1 \\ 
lev_{a,b}(i-1,j-1)+1_{(a_i \neq b_j)}
\end{matrix}
\right. 
\end{cases}
\]

Where \( 1_{(a_i \neq b_j)} \) is 0 if \( a_i = b_j \) and 1 if \( a_i \neq b_j \), and \( lev_{a,b}(i,j) \) represents the distance between the first \( i \) characters of sequence \( a \) and the first \( j \) characters of sequence \( b \).
\
![image](https://github.com/user-attachments/assets/b1f8be25-f7d8-46d6-8fcc-bd1d301daae7)

The smaller the Levenshtein Distance, the more similar the sequences are. If the last characters match, the distance remains unchanged; if they differ, the distance equals the minimum cost of inserting, deleting, or substituting the last character. This approach helps identify similar variables, facilitating the recognition of corresponding information. By applying the Edit Distance algorithm, the system can automatically detect and adjust minor deviations between character sequences, such as variations of the same address or street name. This ensures consistency and uniformity in cadastral data across the entire system, enhancing data management and analysis efficiency.

## **2. Word Embedding**

Word embeddings are mathematical models that encode relationships between words in vector space and are used to standardize cadastral data in the Smart Urban Project. This process relies on unsupervised training, leveraging semantic and syntactic information to create similarity among cadastral terms. For instance, terms like "floor" and "story" may be represented as close vectors due to semantic similarity, allowing the system to automatically group and standardize related information.
\
![image](https://github.com/user-attachments/assets/4321bf18-34d0-4f45-ba33-556a97f099a1)

The embedding algorithm learns an inner-product space to preserve language structure in the cadastral dataset vocabulary. This ensures high consistency and efficiency in cadastral data management, improving the performance of smart urban applications.

In this study, we used two popular text embedding models: E5-small-v2 and GIST. These models have been validated in prior research and shown high effectiveness in capturing text semantics.

- **E5-small-v2:** This version of a transformer-based language model is optimized for performance and processing speed, particularly suitable for cadastral data standardization in the Smart Urban Project. It represents terms as numerical vectors (word embeddings), where semantically similar words have similar vectors in the vector space. This supports error detection and correction in cadastral data, ensuring consistency and accuracy.

  E5-small-v2 employs a Transformer architecture with improvements like Sparse Attention and Knowledge Distillation, enhancing efficiency while maintaining accuracy. The model also handles diverse languages, making it adaptable for multilingual cadastral data standardization.

- **GTE-large:** GTE models, based on the BERT framework, come in three sizes: GTE-large, GTE-base, and GTE-small. They are trained on a large dataset of related text pairs from various domains, making them applicable to tasks like information retrieval and semantic similarity measurement.

  The GTE model undergoes two training stages:
  - **Unsupervised Pre-training:** The model is trained on 800 million text pairs from diverse sources without specific prompts.
  - **Supervised Fine-tuning:** Using smaller datasets annotated by humans, about 3 million data pairs from tasks such as web search and semantic inference are used to improve performance for both symmetric and asymmetric tasks.

This training enables GTE to distinguish texts with similar meanings, supporting cadastral data standardization in the Smart Urban Project and enhancing information management performance and efficiency.

## **3. Cosine Similarity Measure**

Cosine Similarity is a metric for evaluating the similarity between two vectors in an inner-product space. It is calculated as the cosine of the angle between two vectors, reflecting their degree of similarity. If the angle is small (close to 0 degrees), the cosine is near 1, indicating high similarity; if the angle is large (close to 90 degrees), the cosine is near 0, indicating significant differences.

For vectors \( x \) and \( y \), representing the content of two texts, the Cosine Similarity formula is as follows:

\[
\cos(\theta) = \frac{x \cdot y}{||x|| \cdot ||y||}
\]

where \( ||x|| \) and \( ||y|| \) are the magnitudes of vectors \( x \) and \( y \), respectively.
\
![image](https://github.com/user-attachments/assets/564e3890-37fa-4854-bcda-c2442c6f4d4d)

## **4. Research Process**

The overall research process is illustrated in Figure.
\
![image](https://github.com/user-attachments/assets/cd26f3cb-a2e6-47ba-9e06-e56353b491f5)


# II) Research Results

## **1.Study Sample**

The study sample includes data from cadastral databases, Google Maps, and more. The sample data includes the following key information:
- **Street_ID:** A unique identifier for cadastral data, helping to identify each entity in the system.
- **Street_Name:** Content regarding cadastral entity information, including house numbers and street names.

Common errors include: word order mistakes, font errors, added noise words, misspellings, and omitted words. These errors may also co-occur, such as missing words + reordered words, misspellings + missing words, and misspellings + added noise words.
\
![image](https://github.com/user-attachments/assets/022eb854-0235-4129-89ad-69a3d12d828c)

The data sample contains cadastral information from various entities, allowing multidimensional analysis of error types. This sample will be used for analysis and comparison to provide customized recommendations for each subject, such as mitigation and handling methods.

## **2. Accuracy Results**

Similarity between object information:
| Method           | Algorithm/Model       | Accuracy  |
|------------------|-----------------------|-----------|
| Edit Distance    | Levenshtein distance  | 95%       |
| Post Embedding   | Gte-large             | 89%       |
|                  | E5-small-v2           | 86%       |

The accuracy results, based on content similarity of cadastral entities, indicate:
- **Edit Distance** achieved the highest accuracy, at 95.09%. This suggests Edit Distance works effectively in identifying street names, likely because street names differ by only a few characters, and measuring the number of transformations (insertions, deletions, substitutions) between two street name strings helps distinguish them more clearly.
- **Word embedding with the E5 model** had the lowest accuracy at 86.18%. This may imply that street names with semantic similarities are not well represented by this word embedding model, or the E5 model may not be optimized for handling minor character variations in street names.
- **Word embedding with the GTE model** achieved 88.64% accuracy, higher than E5 but still lower than Edit Distance. This result suggests the GTE model better represents word semantics in this context but is still less effective compared to direct character comparison.

# III) Conclusion

Edit Distance is a strong choice for street name identification, especially when differences between names are often at the character level (e.g., differing by one letter or symbol). Word embedding models appear less effective in this case, likely because street names lack complex semantics like ordinary words or sentences, and word embeddings rely more on semantics than character structure.
