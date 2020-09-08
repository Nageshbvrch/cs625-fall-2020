#! /usr/bin/env python3

import sys

from typing import (Callable)
import typing
from fractions import (Fraction)


EPSILON = 10e-6
MAX_ITERATIONS = 100

def newtons_method(f, df, x_n, eps=EPSILON):

    n = 0

    next_x_n = x_n + 1000 * eps
    while abs(x_n - next_x_n) > eps:
        x_n = next_x_n
        next_x_n = x_n - (f(x_n) / df(x_n))

        if n >= MAX_ITERATIONS:
            break

        n += 1

    return x_n


def main():
    try:
        initial_guess = float(sys.argv[1])

    except IndexError as error:
        print("Usage: {0} initial_guess".format(*sys.argv))
        sys.exit(1)

    except ValueError as error:
        print("ERROR {0} is not a valid number".format(*sys.argv))
        print("  " + str(error))
        sys.exit(2)

    # Function (f) and its derivative (dx)
    def f(x):
        return (x ** 2) - 1

    def df(x):
        return 2 * x

    try:
        solution_newton = newtons_method(f, df, initial_guess)
        fx_newton = f(solution_newton)

        print("x = {:.4f} | f(x) = {:.4f}".format(solution_newton, fx_newton))

    except ZeroDivisionError as error:
        print(str(error))


if __name__ == "__main__":
    main()