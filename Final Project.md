# ST114 Final Project
class Data:
    def __init__(self, x, y):
        """ (Data, list, list) -> NoneType

        Create a new data object with two attributes: x and y.
        """
        self.x = x
        self.y = y

    def num_obs(self):
        """ (Data) -> int

        Return the number of observations in the data set.

        >>> data = Data([1, 2], [3, 4])
        >>> data.num_obs()
        2
        """
        return len(self.x)

    def __str__(self):
        """ (Data) -> str
        Return a string representation of this Data in this format:
        x	        y
        18.000          120.000
        20.000          110.000
        22.000          120.000
        25.000          135.000
        26.000          140.000
        29.000          115.000
        30.000          150.000
        33.000          165.000
        33.000          160.000
        35.000          180.000
        """
        output_string = ''
        output_string += 'x\t\ty\n'
        for i in range(len(self.x)-1):
            output_string += '{:.3f}\t\t{:.3f}\n'.format(self.x[i], self.y[i])
        output_string += '{:.3f}\t\t{:.3f}'.format(self.x[-1], self.y[-1])
        return output_string
       

    def compute_sample_means(self):
        """ (Data) -> number, number

        Return sample mean of x and sample mean of y.
        """
        mean_x = sum(self.x) / len(self.x)
        mean_y = sum(self.y) / len(self.y)
        return (mean_x, mean_y)

    def compute_least_squares_fit(self):
        """ (Data) -> number, number

        Return the intercept and slope of the simple linear regression fit
        of the data.
        """
        mean_x, mean_y = self.compute_sample_means()
        Sxx = 0
        Sxy = 0
        for i in range(len(self.x)):
            Sxx += (self.x[i] - mean_x) ** 2
            Sxy += (self.x[i] - mean_x) * (self.y[i] - mean_y)
        beta1 = Sxy / Sxx
        beta0 = mean_y - (beta1 * mean_x)
        return (beta0, beta1)
             

    def compute_SST(self):
        """ (Data) -> number

        Return the sum of squares total (SST).
        """
        mean_x, mean_y = self.compute_sample_means()
        SST = 0
        for i in range(len(self.x)):
            SST += (self.y[i] - mean_y) ** 2
        return SST
