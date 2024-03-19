# Variational-Autoencoder-VAE-
Building a Variational Autoencoder (VAE) functionality for MNIST Dataset and utilising Optuna Hyperparameter tuning feature to identify the best latent layer to identify number images from the dataset. 
This code effectively integrates a VAE model with Optuna for hyperparameter optimization, demonstrating not only model training and evaluation but also the generation and saving of representative images, providing a comprehensive view of the model's capabilities.

## Process
### Defining the VAE Training Function
The function `train_vae` is responsible for building and training the VAE (Variational Autoencoder) model. It takes in the `latent_dim` parameter along with other hyperparameters of the model. The function returns the training history, the encoder part of the VAE, a generator model (decoder) for generating images, and test data with labels.

This function is responsible for building a Variational Autoencoder (VAE) model. It does so by using an encoder network that takes in the input data and encodes it into a latent space. The encoder network consists of multiple layers of neural networks that are designed to learn and extract the most important features of the input data.

Once the input data is encoded into the latent space, a sampling function is applied to select points from the latent space. This is done to introduce stochasticity into the model, which helps in generating diverse outputs. The sampling function is designed to sample points from a probability distribution that is parameterized by the output of the encoder network.

Finally, the selected points are passed through a decoder network that decodes them back into the original data format. The decoder network also consists of multiple layers of neural networks that are designed to learn the inverse mapping of the encoder network. Together, the encoder and decoder networks form the VAE model, which can be trained using a variety of optimization techniques to minimize the reconstruction error.

The model is compiled and trained using the MNIST data.

### 3. Objective Function for Optuna
This function is at the core of the hyperparameter optimization process with Optuna. It receives a trial object from Optuna that suggests a value for latent_dim. The function then calls train_vae with the suggested latent_dim, plots the training and validation loss curves, and visualizes the latent space. Besides, it generates images for digits 0-9 using the VAE and saves these images in a local directory. Finally, the function returns the last validation loss, which Optuna attempts to minimize.

### 4. Optuna Study for Hyperparameter Optimization
An Optuna study is created with the objective to minimize the returned value (validation loss) from the objective function.
study.optimize runs the optimization process for a specified number of trials (n_trials=10).

### 5. Image Generation and Saving
In each trial, after training, the function generates images corresponding to random points in the latent space using the decoder (generator) part of the VAE.
These images are displayed in a Matplotlib figure and saved to a directory named vae_generated_images. The filename indicates the trial number and the latent dimension.

### 6. Directory Management and Plot Saving
os.makedirs ensures that the directory for saving images exists (exist_ok=True allows the code to proceed without error if the directory already exists).
plt.savefig saves the generated images to the specified directory.
plt.close closes the figure after saving to free up memory.

![Trial 9 finished with value: 124.03614044189453 and parameters: {'latent_dim': 6}. Best is trial 4 with value: 111.22822570800781.
Best latent_dim: 18](https://github.com/HarshiniR4/Variational-Autoencoder-VAE-/assets/59364581/10fe977d-afd2-420b-815b-311f86bc570d)
![image](https://github.com/HarshiniR4/Variational-Autoencoder-VAE-/assets/59364581/d295116c-06ba-4daf-b498-b4d4bb3fd7a5)

