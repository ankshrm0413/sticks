# sticks
Chef and his little brother are playing with sticks. They have total N sticks. Length of i-th stick is Ai. 
Chef asks his brother to choose any four sticks and to make a rectangle with those sticks its sides. 
Chef warns his brother to not to break any of the sticks, he has to use sticks as a whole. 
Also, he wants that the rectangle formed should have the maximum possible area among all the rectangles that Chef's brother can make.

Chef's little brother takes this challenge up and overcomes it. Can you also do so? That is, you have to tell whether it is even possible to create a rectangle? 
If yes, then you have to tell the maximum possible area of rectangle.

-----------------------------------------------------------------------------------------------------------------

We need to search for the greatest pair (B, H) such that both B and H occur twice in the array (at least).

From an implementation point of view, it is quite easy since the sticks are at most 10^3. 
Maintain a frequency array of size 10^3, where f(i) contains the frequency of i in the array. 

Go from i = 10^3 down to 1, searching for the two greatest sticks which occur at least twice. 

   for(i = MAX_LENGTH - 1; i >= 1 && second_largest_stick == 0 ; i--) //We keep going till we find the two longest sticks
    {
        if(frequency[i] >= 2)
        {
            if(largest_stick == 0)
                largest_stick = i;
            else if(second_largest_stick == 0)
                second_largest_stick = i;
        }
    }

    printf("%d\n", (second_largest_stick == 0 ? -1 : largest_stick*second_largest_stick));

------------------------------------------------------------------------

I found a bug in this code. It doesn't search for squares ! Hence, I added the square part. 

    for(i = MAX_LENGTH - 1; i >= 1 && second_largest_stick == 0 ; i--) //We keep going till we find the two longest sticks
    {
        if(frequency[i] >= 4)
        {
            if(largest_stick == 0)
                largest_stick = second_largest_stick = i;
            else
                second_largest_stick = i;
        }
        if(frequency[i] >= 2)
        {
            if(largest_stick == 0)
                largest_stick = i;
            else if(second_largest_stick == 0)
                second_largest_stick = i;
        }
    }

    printf("%d\n", (second_largest_stick == 0 ? -1 : largest_stick*second_largest_stick));

-------------------------------------------------------------------------

If the frequency is 0, it is important to check if some other larger stick has already been found. 
For example, consider 

5 5 5 5 7 7 7, Here largest = 7, f(5) = 4 but that doesn't mean we should initalise both sides of a rectangle to 5. That was the other bug. 

Hence, it's important to check if largest = 0 first and then do that, otherwise only initialise one stick.
